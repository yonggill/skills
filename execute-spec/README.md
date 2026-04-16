# execute-spec — 명세 실행 오케스트레이터

`generate-spec`이 만든 기능 명세를 입력으로, 의존성 DAG 기반 3단계 파이프라인(Scaffold → Parallel Feature → Integration)으로 에이전틱하게 구현한다.

## Usage

```
/execute-spec                   # 미완료 Phase 자동 감지 후 이어서 진행
/execute-spec phase-2           # 특정 Phase부터 재시작
```

자연어로 "스펙 실행", "명세 구현", "feature-spec 일괄 구현" 등.

## 3-Phase Pipeline

```
Phase 0. Discovery & DAG  ──→  Phase 1. Scaffold  ──→  Phase 2. Feature  ──→  Phase 3. Integration
   (자동)                     🚦 Gate 1              🚦 Gate 2                🚦 Gate 3
```

| Phase | 병렬 단위 | 서브에이전트 수 | Human Gate |
|------|----------|---------------|-----------|
| 0. Discovery | 스펙 파싱 | 5/배치 | 없음 |
| 1. Scaffold | 자산 카테고리 | 4 병렬 | ✅ Gate 1 |
| 2. Feature | 기능 1개 | 5/배치, 레벨별 | ✅ Gate 2 |
| 3. Integration | 통합 카테고리 | 3 병렬 | ✅ Gate 3 |

## 핵심 원리

- **AC→테스트 선변환**: Phase 2 에이전트는 인수 조건을 테스트로 먼저 만들고 통과시키는 방식으로 구현. 자체 검증 루프를 갖기 때문에 사람이 매번 확인하지 않아도 된다.
- **공유 자산 선고정**: Phase 1에서 타입/스키마/토큰/라우터를 확정해, Phase 2 병렬 에이전트끼리 충돌이 나지 않게 한다.
- **DAG 위상정렬**: 기능 간 의존성을 먼저 펼치고 레벨별로 병렬화. 같은 레벨 안에서는 최대 5개 동시, 배치 간·레벨 간에는 멈추지 않는다.
- **Phase 경계에서만 사람 개입**: 기능 단위 확인은 진행 속도를 무너뜨리므로, 3번의 Human Gate에서만 승인을 받는다.

## 산출물

```
docs/execution/
  manifest.json              # Phase 0 — DAG + 공유 리소스 카탈로그
  phase-1-report.md          # Phase 1 — Scaffold 결과
  phase-2-report.md          # Phase 2 — 기능별 구현 상태
  phase-3-report.md          # Phase 3 — 통합 결과
  logs/<feature-id>/
    test-run.log             # 테스트 실행 로그
    todo.md                  # 변환 불확실 AC 목록
```

구현 코드 위치는 프로젝트 관례를 따른다 (`src/`, `app/`, …). 스킬이 강제하지 않는다.

## 파일 구조

```
~/.claude/skills/execute-spec/
  SKILL.md                                    # 오케스트레이터 본체 (~260 lines)
  README.md
  templates/
    manifest.template.json                    # Phase 0 산출 스키마
    scaffold-contract.template.md             # Phase 1 서브에이전트 프롬프트 골격
    execution-contract.template.md            # Phase 2 서브에이전트 프롬프트 골격
    integration-contract.template.md          # Phase 3 서브에이전트 프롬프트 골격
    phase-report.template.md                  # Human Gate 리포트 템플릿
  references/
    dependency-extraction.md                  # feature-spec → depends_on 추출 규칙
    ac-to-test.md                             # AC → Vitest/Playwright 변환 패턴
    subagent-dispatch.md                      # 배치 크기, 컨텍스트 예산, 실패 처리
```

## generate-spec과의 쌍

| | generate-spec | execute-spec |
|---|---|---|
| 역할 | 기획 문서 생성 | 명세 실행/구현 |
| 산출물 | `docs/specs/**/*.md` | 코드 + `docs/execution/*` |
| 병렬화 | 스펙 작성 병렬 | 구현 병렬 |
| 입력 | 사용자와의 대화 | feature-spec 파일들 |

두 스킬을 순서대로 사용하는 것이 기본 흐름:

```
대화 → generate-spec → 기능 명세 → execute-spec → 구현
```

## Notes

- **Korean-first.** 오케스트레이터 문구와 리포트는 한글. 테스트/코드 주석은 프로젝트 컨벤션 따름.
- **부분 재개.** 모든 Phase는 `manifest.json`의 상태를 보고 미완료 항목만 재개한다.
- **실패한 기능만 재디스패치.** Human Gate 2 이후 일부 기능만 재작업 지시 가능.
- **강제 경로 없음.** 구현 파일 위치는 프로젝트 기존 구조를 존중한다.
