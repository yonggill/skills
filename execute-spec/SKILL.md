---
name: execute-spec
description: Use this skill when feature-specs (docs/specs/feature-specs/**) already exist and the user wants to implement them agentically — or says "스펙 실행", "명세 구현", "execute-spec", "기능 일괄 구현", "feature-spec 구현". Orchestrates a 3-phase pipeline (Scaffold → Parallel Feature Implementation → Integration) with dependency DAG, AC-to-test conversion, and parallel subagent dispatch. Pair with generate-spec — generate-spec produces the specs, execute-spec runs them.
---

# 명세 실행 오케스트레이터

`generate-spec`이 만든 기능 명세(feature-spec)를 입력으로 받아, 의존성 DAG를 구축하고 병렬 서브에이전트로 구현까지 진행하는 3단계 파이프라인이다.

## 설계 원칙 (왜 이렇게 움직이는가)

- **스펙은 계약이다.** 인수 조건(AC)을 실행 가능한 테스트로 **먼저** 변환하면, 구현 에이전트는 테스트 통과로 자체 검증 루프를 가진다. 사람이 매번 확인하지 않아도 된다.
- **공유 자산을 먼저 고정한다.** 병렬 에이전트 간 타입/스키마 충돌은 재작업의 주요 원인이다. Phase 1에서 공통 자산을 단일 소스로 만들고, Phase 2에서는 이를 읽기 전용으로 참조한다.
- **DAG로 펼쳐야 병렬이 가능하다.** 기능 명세 섹션 9·10(연관 기능·크로스 페이지 의존성)을 파싱해 위상정렬한다. 같은 레벨 내 항목은 병렬, 레벨 간은 순차.
- **Phase 경계에만 사람이 개입한다.** 기능 단위 확인은 진행 속도를 무너뜨린다. 레벨 사이·배치 사이에서는 멈추지 않는다. (generate-spec의 "멈춤 금지 규칙"과 동일.)

## 3단계 파이프라인

```
Phase 0. Discovery & DAG (자동)
   └─ feature-specs/** 스캔 → manifest.json 생성

Phase 1. Scaffold (공유 자산 생성)
   ├─ 병렬: 데이터 모델 통합 / 공통 타입 / 디자인 토큰 / 라우터 골격
   └─ 🚦 Human Gate 1: Scaffold 승인

Phase 2. Feature 구현 (DAG 위상정렬, 레벨별 병렬 배치)
   ├─ 레벨 1: 의존성 없는 기능들 — 배치당 최대 5개 병렬
   ├─ 레벨 2: 레벨 1에 의존하는 기능들 — 배치당 최대 5개 병렬
   ├─ ...
   └─ 각 기능 에이전트: AC→test 선변환 → 구현 → 테스트 통과까지 자체 루프
   └─ 🚦 Human Gate 2: 구현 결과 리뷰 (Phase 2 전체 완료 후 1회)

Phase 3. Integration (전역 통합 & E2E)
   ├─ 네비게이션 연결 / 전역 상태 / 페이지 간 데이터 흐름
   ├─ E2E 테스트 실행
   └─ 🚦 Human Gate 3: 최종 승인
```

## 진입 흐름

### 1. 전제조건 스캔

Glob으로 다음을 확인한다:

- `docs/specs/feature-specs/**/*.md` — 최소 1개 이상 필요 (없으면 generate-spec 실행 안내)
- `docs/specs/page-specs/**/*.md` — 페이지 명세 (있으면 Phase 3 Integration 품질 상승)
- `docs/execution/manifest.json` — 이미 Phase 0이 돌았는지

### 2. 진행 상태 표시

```
🚀 명세 실행 - 현재 진행 상태

  ✅ Phase 0. Discovery & DAG        (manifest.json 존재, 기능 23개)
  ✅ Phase 1. Scaffold               (Human Gate 1 통과, 공유 자산 12개)
  🟡 Phase 2. Feature 구현           (14/23 완료, 레벨 3/4 진행 중)
  ⬜ Phase 3. Integration

어떤 Phase부터 진행할까요? (기본: 이어서 Phase 2)
```

Phase 2가 부분 진행 중일 때는 `docs/execution/manifest.json`의 `phase_status.features`에서 완료된 기능을 제외하고 재개한다.

### 3. 의존성 검증

선택한 Phase가 이전 Phase 산출물을 요구하는데 없으면 경고:

```
⚠️ Phase 2는 Phase 1의 공유 자산이 필요합니다. Phase 1부터 진행할까요?
```

## Phase 0: Discovery & DAG

**목적**: 모든 feature-spec을 파싱해 의존성 그래프와 공유 리소스 카탈로그를 만든다.

### 실행 방식

1. `docs/specs/feature-specs/**/*.md` 전체를 Glob
2. 스펙을 배치로 묶어 **병렬 서브에이전트**로 파싱 (배치당 최대 5개)
3. 각 서브에이전트의 파싱 결과를 병합해 `docs/execution/manifest.json` 생성

### 서브에이전트 프롬프트 (Phase 0 파서)

**읽을 파일**: `templates/manifest.template.json` (스키마 참조)

서브에이전트에게 전달:

```
역할: feature-spec 파서.
입력 파일들: <feature-spec 경로 배열>
출력: 각 파일당 JSON 객체 — { id, path, title, depends_on, shared_resources, complexity, us_ac_count }
추출 규칙:
- title: 첫 # 헤딩
- depends_on: 섹션 10 "선행 페이지" 테이블의 페이지 ID 또는 섹션 9의 연관 기능
- shared_resources.tables: 섹션 4의 테이블 이름
- shared_resources.apis: 섹션 5의 METHOD + path
- shared_resources.types: 섹션 5의 TypeScript interface 이름
- complexity: 섹션 14의 "복잡도" 값, 없으면 "medium"
- us_ac_count: 섹션 2의 AC-N 개수
질문 금지. 파싱만 하라.
```

### 산출물

`docs/execution/manifest.json` — `templates/manifest.template.json` 스키마 참조.

## Phase 1: Scaffold

**목적**: Phase 2 병렬 구현 전에 타입/스키마 충돌을 방지할 공유 자산을 먼저 만든다.

### 실행 방식

manifest의 `shared` 섹션을 기반으로 **4개 서브에이전트를 병렬 디스패치**:

| 에이전트 | 입력 | 출력 |
|---------|------|------|
| Schema Consolidator | 모든 스펙의 섹션 4 | `db/migrations/*.sql` 또는 `prisma/schema.prisma` 업데이트 |
| Type Generator | 모든 스펙의 섹션 5 | `src/types/api.ts` (shared request/response types) |
| Design Token Extractor | 모든 스펙의 섹션 3 시각 디자인 스펙 | `src/styles/tokens.ts` |
| Router Skeleton | 페이지 목록 (`docs/specs/pages/*.md`) | `src/app/` 또는 `src/routes/` 빈 파일 + 라우터 등록 |

각 에이전트 프롬프트는 `templates/scaffold-contract.template.md` 참조.

### Human Gate 1

모든 Phase 1 에이전트 완료 후, `docs/execution/phase-1-report.md`를 생성해 사용자에게 제시한다:

- 생성/수정된 파일 목록
- 충돌/경고 (예: 같은 테이블에 서로 다른 컬럼 정의)
- 다음 Phase 2가 읽기 전용으로 참조할 경로들

사용자 승인 후 Phase 2로 진행. 승인 전에 다음 Phase로 **절대** 넘어가지 않는다.

## Phase 2: Feature 구현 (핵심)

**목적**: 각 feature-spec을 독립 구현 단위로 보고, DAG 순서에 따라 최대한 병렬로 완성한다.

### 실행 흐름

```
1. manifest의 DAG를 위상정렬 → 레벨 리스트 생성
2. 각 레벨을 순차 처리
3. 레벨 내부에서 배치 (최대 5개 기능/배치) 구성
4. 배치 내부는 병렬 디스패치
5. 배치 완료 후 다음 배치, 레벨 완료 후 다음 레벨 — 중단 없이 연속 진행
6. Phase 2 전체 완료 후 Human Gate 2
```

### 각 기능 서브에이전트의 작업 순서

한 명의 구현 에이전트에게 한 기능(feature-spec 1개)을 맡긴다. 에이전트의 내부 루프:

```
Step 1. AC → test 변환
   - 섹션 2의 모든 AC-N을 `references/ac-to-test.md` 패턴에 따라 테스트 파일로 변환
   - 변환 불확실한 AC는 test.todo()로 남기고 TODO 리포트에 기록

Step 2. 테스트 실행 (당연히 실패)
   - 테스트 파일 저장 후 1차 실행하여 실패를 확인 — 테스트가 실제로 돌아가는지 검증

Step 3. 구현
   - 섹션 3 컴포넌트 계층, 섹션 4 데이터 모델, 섹션 5 API, 섹션 6 비즈니스 로직을 참조
   - 공유 타입은 Phase 1 산출물에서 import (절대 재정의 금지)
   - 섹션 3 "5가지 화면 상태" 모두 구현 (Empty/Loading/Partial/Error/Ideal)

Step 4. 테스트 재실행
   - 모든 테스트 통과까지 루프 (최대 5회)
   - 5회 후에도 실패하면 실패 리포트와 함께 종료 (사람 개입 필요)

Step 5. 구현 리포트 반환
   - 생성/수정 파일 목록
   - 테스트 통과/실패 요약
   - TODO로 남긴 AC 목록
```

에이전트 프롬프트 골격: `templates/execution-contract.template.md`.
AC 변환 규칙: `references/ac-to-test.md`.

### 배치 크기와 멈춤 금지

- **최대 동시 서브에이전트**: 5개
- 레벨 내 기능이 5개 초과면 5개씩 배치로 나누어 **순차 디스패치 (배치 내부는 병렬)**
- **배치 간에도 멈추지 않고 연속 진행한다.** 중간에 사용자 확인을 요청하지 않는다.
- 레벨 간에도 마찬가지. Phase 2 전체가 끝날 때까지 한 번도 멈추지 않는다.

### 레벨이 여러 개일 때 진행 예시

```
Level 1 (4 features, 의존성 없음)
  └─ 배치 1: [f1, f2, f3, f4] 병렬 → 모두 완료
Level 2 (7 features, 레벨 1에 의존)
  └─ 배치 1: [f5, f6, f7, f8, f9] 병렬 → 완료
  └─ 배치 2: [f10, f11] 병렬 → 완료
Level 3 (2 features)
  └─ 배치 1: [f12, f13] 병렬 → 완료

→ Phase 2 완료 → Human Gate 2
```

### Human Gate 2

Phase 2 전체 완료 후 `docs/execution/phase-2-report.md` 생성:

- 기능별 상태 (✅ 완료 / ⚠️ 일부 테스트 미통과 / ❌ 실패)
- 전체 테스트 통과율
- TODO로 남은 AC 목록
- 공유 자산 변경이 필요했던 기능 (있었다면 경고)

사용자가 리뷰 후 승인/재작업 지시. 재작업은 **실패한 기능만** 재디스패치.

## Phase 3: Integration

**목적**: 개별 기능들이 페이지와 앱 레벨에서 유기적으로 동작하는지 확인.

### 작업 항목

1. **네비게이션 통합**: 페이지 명세의 진입/이탈 경로에 따라 링크·라우터 연결
2. **전역 상태 통합**: 로그인/세션/알림 등 앱 공통 상태가 기능들과 맞물리는지
3. **크로스 페이지 데이터 흐름 검증**: manifest의 `depends_on`에 명시된 데이터 전달이 실제로 되는지
4. **E2E 테스트 실행**: 섹션 12의 E2E 시나리오가 있으면 Playwright로 전체 실행

### 서브에이전트 분배

- Navigation Integrator: 1개
- Global State Integrator: 1개
- E2E Runner: 1개

병렬 디스패치, 모두 완료 후 `docs/execution/phase-3-report.md` 생성.

### Human Gate 3

최종 승인. 승인 시 `docs/execution/manifest.json`의 전체 상태를 `completed`로 마킹.

## 멈춤 금지 규칙 (CRITICAL)

generate-spec과 동일하게 다음을 엄격히 지킨다.

**금지**:
- ❌ 배치 내 한 기능 완료 후 "다음 기능으로 진행할까요?" 질문
- ❌ 레벨 간 이동 전 사용자 확인 요청
- ❌ "시간이 오래 걸릴 수 있습니다" 경고 후 재확인
- ❌ 일부 기능만 하고 중단
- ❌ Phase 내부에서 어떤 이유로든 사용자에게 확인 요청

**허용**:
- ✅ Phase 최초 진입 시 1회 의사 확인
- ✅ Phase 경계에서 Human Gate 통해 승인 요청
- ✅ 사용자가 **명시적으로** 중단을 요청한 경우
- ✅ 서브에이전트가 5회 재시도 후에도 실패 시 해당 기능만 스킵 (전체는 계속 진행)

## 산출물 디렉토리 구조

```
docs/
  specs/                              # generate-spec의 산출물 (입력)
    feature-specs/...
    page-specs/...
  execution/                          # execute-spec의 산출물
    manifest.json                     # Phase 0
    phase-1-report.md                 # Phase 1
    phase-2-report.md                 # Phase 2
    phase-3-report.md                 # Phase 3
    logs/
      <feature-id>/
        test-run.log
        todo.md
```

구현 코드의 위치는 프로젝트 컨벤션을 따른다 (`src/`, `app/`, `components/` 등). 스킬이 경로를 강제하지 않고, 프로젝트 기존 구조를 Glob으로 탐지한 뒤 따른다.

## 참조 문서

| 파일 | 언제 읽는가 |
|------|----------|
| `templates/manifest.template.json` | Phase 0에서 manifest 생성 시 |
| `templates/scaffold-contract.template.md` | Phase 1 서브에이전트 프롬프트 구성 시 |
| `templates/execution-contract.template.md` | Phase 2 서브에이전트 프롬프트 구성 시 |
| `templates/integration-contract.template.md` | Phase 3 서브에이전트 프롬프트 구성 시 |
| `templates/phase-report.template.md` | Human Gate 리포트 생성 시 |
| `references/dependency-extraction.md` | manifest의 depends_on 필드를 어떻게 채우는지 |
| `references/ac-to-test.md` | AC 문장을 테스트 코드로 바꾸는 패턴 |
| `references/subagent-dispatch.md` | 배치 크기, 컨텍스트 예산, 실패 처리 상세 |

## generate-spec과의 관계

`execute-spec`은 `generate-spec`의 자매 스킬이다. 다음 정보를 **암묵적으로 신뢰**한다:

- feature-spec의 섹션 번호와 구조 (1~14)
- AC는 `[ ] AC-N: ...` 형식
- frontmatter의 `depends-on` 필드
- 디렉토리 구조 (`docs/specs/...`)

generate-spec 산출물이 아닌 임의의 마크다운을 입력으로 받으면 파싱 오류가 날 수 있다. 그 경우 사용자에게 형식 차이를 알리고 중단한다.
