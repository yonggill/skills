# AC → Test Conversion Patterns

Phase 2 서브에이전트가 feature-spec의 인수 조건(AC)을 테스트로 변환할 때 참조한다.

## 핵심 원리

AC는 "사람이 읽고 확인하는 문장"이고 테스트는 "기계가 실행하는 검증"이다. 완벽히 기계화할 수 없는 AC가 반드시 존재한다. 기계화가 어려운 경우 `test.todo()`로 남기고 `todo.md`에 이유를 기록한다 — 이것도 가치 있는 산출물이다.

> **왜 test.todo를 쓰는가**: 완벽하지 못한 테스트를 억지로 만드는 것보다, "이 AC는 기계화 안 됨"을 명시적으로 남기는 편이 낫다. 리뷰어가 수동 검증 대상을 바로 알 수 있다.

## 변환 패턴 카탈로그

### 1. UI 상호작용 (클릭/입력/선택)

**AC 형태**: "X 버튼을 클릭하면 Y가 표시된다", "N자 이상 입력 시 검색 결과가 나타난다"

**변환**: Testing Library + userEvent

```
AC: "편집 버튼 클릭 시 편집 모달이 열린다"

→
it('편집 버튼 클릭 시 편집 모달이 열린다', async () => {
  const user = userEvent.setup();
  render(<FeatureComponent />);
  await user.click(screen.getByRole('button', { name: /편집/ }));
  expect(screen.getByRole('dialog', { name: /편집/ })).toBeInTheDocument();
});
```

**주의**: 정확한 이름/role을 스펙의 컴포넌트 계층(섹션 3)에서 추출. 추측 금지.

### 2. 상태 전이

**AC 형태**: "상태가 PENDING에서 APPROVED로 전환된다", "승인 시 audit_log에 기록된다"

**변환**: 상태 변화 검증 또는 함수 단위 테스트

```
AC: "승인 버튼 클릭 시 계약 상태가 PENDING → APPROVED로 변경된다"

→
it('승인 시 상태가 APPROVED로 변경된다', async () => {
  const contract = { id: 'c1', status: 'PENDING' };
  const result = await approveContract(contract);
  expect(result.status).toBe('APPROVED');
});
```

### 3. API 응답

**AC 형태**: "정상 응답 시 N건의 데이터가 렌더링된다", "404 응답 시 에러 배너가 표시된다"

**변환**: MSW (Mock Service Worker) mock + fetch 테스트

```
AC: "GET /api/notifications 404 응답 시 '알림을 불러올 수 없습니다' 배너가 표시된다"

→
it('404 응답 시 에러 배너 표시', async () => {
  server.use(
    http.get('/api/notifications', () => HttpResponse.json({}, { status: 404 }))
  );
  render(<NotificationList />);
  expect(await screen.findByText('알림을 불러올 수 없습니다')).toBeInTheDocument();
});
```

정확한 에러 메시지는 섹션 8 (에러 처리) 테이블에서 인용한다. 추측 금지.

### 4. 폼 유효성 검사

**AC 형태**: "필수 필드가 비어있으면 저장 버튼 비활성화", "이메일 형식이 아니면 에러 메시지 표시"

**변환**: 입력 + DOM 상태 검증

```
AC: "제목이 비어있으면 저장 버튼이 비활성화된다"

→
it('제목 빈칸일 때 저장 버튼 비활성', async () => {
  const user = userEvent.setup();
  render(<Form />);
  const save = screen.getByRole('button', { name: /저장/ });
  expect(save).toBeDisabled();
  await user.type(screen.getByLabelText(/제목/), 'hi');
  expect(save).toBeEnabled();
});
```

### 5. 비어있음/로딩/에러 상태

**AC 형태**: "데이터 0건일 때 '알림이 없습니다' 표시", "로딩 중 스켈레톤 표시"

**변환**: 각 상태를 별도의 test case로

```
describe('화면 상태', () => {
  it('Empty: 데이터 0건일 때 빈 상태 메시지', async () => {
    server.use(http.get('/api/x', () => HttpResponse.json({ items: [] })));
    render(<X />);
    expect(await screen.findByText('데이터가 없습니다')).toBeInTheDocument();
  });

  it('Loading: API 응답 대기 중 스켈레톤', () => {
    server.use(http.get('/api/x', () => new Promise(() => {}))); // never resolve
    render(<X />);
    expect(screen.getByTestId('skeleton')).toBeInTheDocument();
  });

  it('Error: API 실패 시 에러 UI', async () => {
    server.use(http.get('/api/x', () => HttpResponse.error()));
    render(<X />);
    expect(await screen.findByText(/다시 시도/)).toBeInTheDocument();
  });
});
```

5가지 화면 상태 **모두** 테스트로 확보. 누락 시 구현도 누락된 것으로 간주한다.

### 6. 성능 (Nms 이내) — TODO 처리

**AC 형태**: "클릭 시 500ms 이내 렌더링", "검색 결과 300ms 이내 업데이트"

**변환**: test.todo + todo.md 기록

```
AC: "필터 변경 시 300ms 이내 결과 업데이트"

→
test.todo('필터 변경 300ms 이내 업데이트 — 성능 AC는 자동 측정 미지원');
```

todo.md:
```
## 성능 AC
- AC-5: 필터 변경 300ms — Lighthouse CI 또는 수동 측정으로 별도 검증 필요
```

### 7. 접근성

**AC 형태**: "키보드로 모든 액션 접근 가능", "스크린리더로 레이블 읽힘", "대비 비율 4.5:1 이상"

**변환**: 가능한 범위에서 jest-axe 또는 Testing Library, 어려운 것은 TODO

```
AC: "키보드로 전체 폼 조작 가능"

→
it('키보드로 탭 이동', async () => {
  const user = userEvent.setup();
  render(<Form />);
  await user.tab();
  expect(screen.getByLabelText(/제목/)).toHaveFocus();
  await user.tab();
  expect(screen.getByLabelText(/내용/)).toHaveFocus();
});

AC: "색 대비 4.5:1 이상"

→
test.todo('색 대비 4.5:1 — Lighthouse/axe 별도 검증');
```

### 8. 시간/날짜 관련

**AC 형태**: "오늘 이후 날짜만 선택 가능", "1시간 경과 시 세션 만료"

**변환**: vi.useFakeTimers / jest.useFakeTimers

```
AC: "세션 시작 후 1시간 경과 시 자동 로그아웃"

→
it('1시간 경과 시 자동 로그아웃', async () => {
  vi.useFakeTimers();
  render(<App />);
  login();
  vi.advanceTimersByTime(60 * 60 * 1000);
  await waitFor(() => expect(mockNavigate).toHaveBeenCalledWith('/login'));
  vi.useRealTimers();
});
```

### 9. 권한/역할별 동작

**AC 형태**: "관리자만 삭제 버튼 표시", "일반 사용자는 읽기 전용"

**변환**: 역할별 렌더링을 각각 테스트

```
describe('권한', () => {
  it('관리자: 삭제 버튼 표시', () => {
    render(<X />, { wrapper: withUser({ role: 'admin' }) });
    expect(screen.getByRole('button', { name: /삭제/ })).toBeInTheDocument();
  });
  it('일반 사용자: 삭제 버튼 숨김', () => {
    render(<X />, { wrapper: withUser({ role: 'user' }) });
    expect(screen.queryByRole('button', { name: /삭제/ })).not.toBeInTheDocument();
  });
});
```

## 변환 실패/TODO 판단 기준

다음 중 하나라도 해당하면 `test.todo()` + todo.md 기록:

- **정량적 성능 요구** (Xms 이내) — 단위 테스트에서 측정 불가
- **시각적 대비/색 정확도** — 기계화 어려움
- **사용자 체감 품질** ("자연스럽게", "부드럽게", "사용자가 쉽게 이해") — 주관적
- **외부 시스템 실제 호출** ("실제 결제가 이뤄진다") — 테스트 환경에서 금지
- **스펙 문장 모호** — 해석이 여러 갈래로 가능

todo.md 형식:

```markdown
## AC-3: 필터 변경 시 300ms 이내 결과 업데이트
- 이유: 성능 AC는 단위 테스트에서 정확 측정 불가
- 권장: Lighthouse CI 또는 production-like 환경에서 수동 측정

## AC-7: 색 대비 4.5:1 이상
- 이유: jest-axe로 부분 커버 가능하나 다크모드 등 조합에서 불완전
- 권장: Playwright + axe-playwright로 E2E 레벨 검증
```

## 테스트 파일 배치

프로젝트 관례 탐지 후 결정:

- `*.test.tsx` (컴포넌트 옆) — Vitest/Jest 기본
- `__tests__/*.test.ts` — 디렉토리 분리
- `tests/unit/`, `tests/integration/` — 프로젝트 명시적 구조

기존 테스트 파일 패턴을 Glob으로 먼저 살펴본 뒤 일치시킨다.

## 스펙 섹션 12와의 관계

섹션 12 "테스트 계획"은 AC보다 상위의 시나리오 설명이다 (UT-01, IT-01, E2E-01 ID 부여).

- UT (Unit Test) → 이 문서의 패턴으로 구현
- IT (Integration Test) → 여러 컴포넌트 + API 결합 테스트로 구현
- E2E → Playwright/Cypress로 별도 작성, Phase 3 E2E Runner가 담당

AC 테스트(Step 2 ~ Step 5) 와 섹션 12 테스트(Playwright E2E는 Phase 3에서)를 **중복으로 작성하지 않는다** — 레벨이 다르다.
