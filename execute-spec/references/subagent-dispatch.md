# Subagent Dispatch — 배치 크기, 컨텍스트 예산, 실패 처리

오케스트레이터(메인 에이전트)가 서브에이전트를 효율적으로 디스패치하기 위한 상세 가이드.

## 배치 크기

**최대 동시 서브에이전트**: 5개

이유:
- 대부분의 환경에서 병렬성 수익이 체감되는 상한 (5개 이상은 경합/API 제약으로 순증이 미미)
- 배치 단위로 리포트를 모으는 루틴이 단순해짐
- 리소스 사용량 예측 가능

**예외**: 매우 경량 작업 (Phase 0 파서) 은 7~8개까지도 가능하지만 기본 5 유지.

## 레벨 × 배치 디스패치 패턴

Phase 2 기준:

```
Level 1 (10 features):
  Batch 1: [f01, f02, f03, f04, f05] 병렬 → 완료 대기
  Batch 2: [f06, f07, f08, f09, f10] 병렬 → 완료 대기
  (Level 1 완료, 바로 Level 2 진행 — 사용자 확인 금지)

Level 2 (3 features):
  Batch 1: [f11, f12, f13] 병렬 → 완료 대기
  (Level 2 완료)

→ Phase 2 종료, Human Gate 2
```

**배치 간에 사용자 확인하지 않는다.** 레벨 간도 마찬가지. Phase 전체가 끝나야 사람이 개입한다.

## 컨텍스트 예산 (서브에이전트당 입력 토큰 관리)

Phase 2 서브에이전트는 다음을 읽는다:

| 파일 | 대략 토큰 |
|------|----------|
| feature-spec (섹션 1~14) | 4,500 ~ 10,000 |
| page-spec | 2,500 ~ 3,500 |
| ac-to-test.md | ~2,000 |
| shared_types (부분 읽기) | 500 ~ 2,000 |
| shared_schema (부분 읽기) | 500 ~ 2,000 |

합계: 약 10,000 ~ 20,000 토큰. 서브에이전트 컨텍스트 내에서 여유 있게 수용 가능.

**토큰 절약 팁**:
- shared_types/schema는 해당 기능이 쓰는 타입만 grep으로 찾아서 전달
- page-spec은 해당 섹션만 (섹션 3, 섹션 5 중심)
- ac-to-test.md는 Read로 로드 (템플릿이 이미 지시)

## 로그 디렉토리 구조

각 서브에이전트의 출력을 정해진 위치에 저장:

```
docs/execution/logs/
  phase-0/
    parser-batch-1.log
    parser-batch-2.log
  phase-1/
    schema-consolidator.log
    type-generator.log
    design-token-extractor.log
    router-skeleton.log
  phase-2/
    01-notification-center/
      01-notification-list-view/
        test-run.log
        todo.md
        agent-output.json
  phase-3/
    navigation-integrator.log
    global-state-integrator.log
    e2e-runner.log
```

오케스트레이터는 이 경로를 **서브에이전트 프롬프트에 명시**하여 각자 자기 로그를 쓰게 한다.

## 실패 처리

### 서브에이전트 실패 시나리오

| 실패 유형 | 조치 |
|-----------|------|
| 타임아웃 | 해당 기능만 `status: failed`로 manifest 업데이트, 전체 계속 진행 |
| 테스트 5회 재시도 후 실패 | 동일 — 해당 기능만 failed |
| shared 자산 부족 (타입 없음 등) | 해당 기능만 `status: blocked`, Phase 1 재실행 제안 |
| JSON 리포트 파싱 실패 | 해당 기능 failed, agent-output.log 전체를 리포트에 포함 |
| 메시지 도중 중단 (프로세스 죽음) | failed로 간주, 재개 시 재디스패치 후보 |

**공통 원칙**: 한 기능의 실패가 다른 기능의 실행을 막지 않는다. 오케스트레이터는 배치의 나머지를 끝까지 진행하고, Human Gate 리포트에 실패 목록을 모아 보고.

### 의존성 위반

A가 B에 의존하는데 B가 실패했다면 A는 어떻게?

- **기본**: A를 디스패치하되 B의 산출물이 없으면 A도 실패할 가능성이 높음을 로그
- **대안 1 (엄격)**: B 실패 시 A는 자동 스킵, manifest에 `blocked_by: B`
- **대안 2 (허용적)**: A도 시도 — 같은 페이지 다른 기능의 AC만 검증하는 게 가능할 수 있음

권장: **엄격 모드**. B 실패 시 A는 blocked 처리해서 Human Gate 2에서 의사결정.

## 재개 (resume) 흐름

Phase 2가 중간에 멈췄다가 다시 시작될 때:

1. manifest.json의 `phase_status.phase_2_features.per_feature`를 읽음
2. `completed` 상태인 기능은 스킵
3. `pending | failed | blocked` 상태 기능만 대상
4. DAG 위상정렬은 재계산하지 않음 (manifest의 level 값 재사용)
5. 레벨별로 배치 다시 구성해서 디스패치

> **주의**: 재개 시 `failed` 상태를 자동으로 재시도할지 말지는 사용자 의사에 따름. 기본은 **재시도 안 함** (Human Gate에서 명시 지시 필요).

## 진행 표시

사용자에게 배치 진행을 텍스트로 짧게 알린다:

```
Phase 2 / Level 1 / Batch 1 (5/10 features) — 시작
  ├─ 01-notification-center/01-notification-list-view
  ├─ 01-notification-center/02-notification-rule-settings
  ├─ 02-help/01-guide-list-and-detail
  ├─ 03-settings/01-profile-edit
  └─ 04-dashboard/01-summary

Batch 1 완료: ✅ 4 / ⚠️ 1 → Batch 2 시작
```

**배치 완료 때마다 1줄**, 사용자 질문 없이 계속 진행.

## 배치 병렬 디스패치 — 실수 방지

Agent tool 호출이 **하나의 메시지에서 여러 개** 있어야 실제로 병렬 실행된다.

**잘못된 예** (순차):
```
turn N:   Agent(feature f01)
turn N+1: (f01 완료) → Agent(feature f02)
turn N+2: (f02 완료) → Agent(feature f03)
```
이러면 5개가 아니라 1개씩 직렬.

**올바른 예** (병렬):
```
turn N: [
  Agent(feature f01),
  Agent(feature f02),
  Agent(feature f03),
  Agent(feature f04),
  Agent(feature f05)
]
turn N+1: (5개 모두 완료됨) → 다음 배치 5개 동시 디스패치
```

오케스트레이터 구현 시 **반드시 하나의 응답에서 여러 Agent 호출**을 낸다.
