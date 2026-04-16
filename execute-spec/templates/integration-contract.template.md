# Phase 3 서브에이전트 계약 (Integration)

Phase 3에서는 3개 서브에이전트를 병렬 디스패치한다.

---

## 1. Navigation Integrator

```
역할: 페이지 명세의 진입/이탈 경로를 실제 네비게이션 코드로 연결한다.

입력:
- manifest_path
- page_specs_glob: docs/specs/page-specs/**/00-page-spec.md
- project_root

작업:
1. 각 page-spec의 "진입 경로", "이탈 경로" 섹션 파싱
2. Phase 1에서 생성된 라우터 파일을 기반으로 실제 링크·리다이렉트·가드 추가
3. 네비게이션 메뉴 컴포넌트 (Sidebar/Header/Breadcrumb) 업데이트
4. 권한 기반 라우트 가드 필요 시 스펙의 "역할별 동작" 참조

출력:
- 수정 파일 목록
- 연결되지 못한 경로 목록 (페이지가 아직 없거나 경로 애매)
```

---

## 2. Global State Integrator

```
역할: 크로스 페이지 데이터 흐름과 전역 상태를 실제로 연결한다.

입력: manifest + feature_specs + project_root

작업:
1. 각 feature-spec의 "섹션 10: 크로스 페이지 의존성"에서 데이터 흐름 추출
2. 전역 상태 스토어(Zustand/Jotai/Redux/React Context 등) 탐지
3. 페이지 간 전달 데이터가 URL 파라미터/검색 파라미터/스토어 중 어디로 가야 하는지 판단
4. 연결 코드 작성
5. 로그인 세션·권한·알림 등 앱 공통 상태는 기능들과 실제로 맞물리는지 검증

출력:
- 수정 파일 목록
- 연결 불가 흐름 리포트 (스펙 해석 어려운 경우)
```

---

## 3. E2E Runner

```
역할: 각 feature-spec의 "섹션 12: 테스트 계획 - E2E" 시나리오를 실행하고 결과를 모은다.

입력: manifest + feature_specs + project_root

작업:
1. 프로젝트의 E2E 도구 탐지 (Playwright/Cypress)
2. 이미 작성된 E2E 테스트 파일을 Glob으로 수집
3. 스펙에 있는 E2E 시나리오 중 자동화 되지 않은 것 식별
4. 자동화된 것들을 headless 모드로 실행
5. 실패 케이스는 screenshot/trace 수집

출력:
- 실행된 테스트 수 / 통과 / 실패
- 실패 상세 (feature_id 매핑)
- 자동화 누락 시나리오 목록
```

---

## 공통 계약

- **앱 빌드가 가능해야 한다** — 통합 작업 완료 후 `npm run build` 또는 동등한 명령이 통과해야 함
- **타입 에러 0** — tsc --noEmit 통과가 Phase 3 완료 조건
- **E2E 실패는 치명적이지 않음** — 개별 기능의 unit test는 이미 Phase 2에서 통과했으므로, E2E 실패는 리포트만 하고 계속 진행
- **사용자 확인 금지** — Phase 3 전체 완료 후 Human Gate 3에서만 응답

## 오케스트레이터 체크리스트

3개 에이전트 병렬 디스패치.
모두 완료 후 phase-3-report.md 생성 → Human Gate 3.
