# Phase {N} Report

> 이 템플릿을 복사해 `docs/execution/phase-{N}-report.md`로 저장한다.
> Human Gate에서 사용자가 승인/재작업을 결정하는 근거 문서이므로, **사실만** 기록한다.

---

## Phase 개요

- **Phase**: {0: Discovery / 1: Scaffold / 2: Features / 3: Integration}
- **시작 시각**: YYYY-MM-DD HH:MM
- **완료 시각**: YYYY-MM-DD HH:MM
- **서브에이전트 수**: N
- **전체 상태**: ✅ Clean / 🟡 Partial / ❌ Blocked

## 실행 요약

| 지표 | 값 |
|------|----|
| 생성된 파일 | N |
| 수정된 파일 | N |
| 발견된 충돌 | N |
| 미해결 TODO | N |

## Phase 별 필수 항목

### Phase 1 (Scaffold)

- [ ] Schema Consolidator 완료 — 테이블 N개 / 충돌 N개
- [ ] Type Generator 완료 — interface N개 / 충돌 N개
- [ ] Design Token Extractor 완료 — 토큰 N개
- [ ] Router Skeleton 완료 — 페이지 N개

**충돌 상세**: (스키마/타입 충돌이 있으면 테이블로)

| 자산 | 충돌 위치 | 스펙 A | 스펙 B | 권장 해결 |
|------|----------|--------|--------|----------|
| ... | ... | ... | ... | ... |

**Human Gate 1 결정 항목**:
- 충돌 해결 방향
- 공유 자산 배치 경로 승인
- 다음 Phase 진행 여부

---

### Phase 2 (Features)

**레벨별 요약**:

| 레벨 | 기능 수 | 완료 | 부분 | 실패 |
|------|--------|------|------|------|
| 1 | N | N | N | N |
| 2 | ... | ... | ... | ... |

**기능별 상세**:

| 기능 ID | 상태 | AC 통과 | AC TODO | AC 실패 | 테스트 파일 | 비고 |
|---------|------|--------|---------|---------|------------|------|
| 01-foo/01-bar | ✅ | 7 | 0 | 0 | src/... | |
| 01-foo/02-baz | 🟡 | 5 | 2 | 0 | src/... | 성능 AC는 TODO |
| 02-qux/01-zot | ❌ | 3 | 0 | 4 | src/... | 5회 재시도 실패 |

**전체 테스트 통과율**: N / N (N%)

**TODO로 남은 AC**: (기능 ID별로 묶어서)

- 01-foo/02-baz
  - AC-3: "렌더링 500ms 이내" — 성능 AC는 자동 검증 어려움
  - AC-7: "접근성 — 스크린리더 레이블" — axe 규칙 매핑 불확실

**실패 기능 상세**: (각 실패 기능의 마지막 test-run.log 요약)

**Human Gate 2 결정 항목**:
- 실패 기능 재디스패치 / 스킵 / 수동 개입
- TODO AC 처리 방향
- Phase 3 진행 여부

---

### Phase 3 (Integration)

- [ ] Navigation Integrator — 연결 N개 / 미연결 N개
- [ ] Global State Integrator — 흐름 N개 / 불가 N개
- [ ] E2E Runner — 실행 N개 / 통과 N개 / 실패 N개

**빌드 체크**:
- [ ] `tsc --noEmit` 통과
- [ ] 프로덕션 빌드 명령 통과

**E2E 실패 목록**: (실패 시 스크린샷/트레이스 경로)

**Human Gate 3 결정 항목**:
- E2E 실패 수용 가능 여부
- 전체 배포 준비 상태 최종 승인

---

## 다음 액션 제안

> 리포트 작성 시 자동으로 채운다. 사용자가 선택하기 쉽도록 구체적인 옵션을 제시.

**옵션 A** (권장): ...
**옵션 B**: ...
**옵션 C** (중단): 사용자가 수동 처리 후 재개

---

## 부록: 로그 위치

- Phase 서브에이전트 출력: `docs/execution/logs/<phase>/<agent>.log`
- Feature 테스트 로그: `docs/execution/logs/<feature-id>/test-run.log`
- Feature TODO: `docs/execution/logs/<feature-id>/todo.md`
