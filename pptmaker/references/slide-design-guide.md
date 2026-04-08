# Slide Design Guide

Phase 2.5에서 각 슬라이드의 풀 스펙을 작성할 때 참조하는 가이드. 이 문서의 규칙을 따라 `{topic}-slide-specs.md`의 각 슬라이드 블록을 작성한다.

---

## 1. 스펙 블록 포맷

각 슬라이드는 아래 필드를 모두 포함해야 한다. 생략 금지.

```
### Slide N: {제목}

**Role:** (1줄) 슬라이드의 역할과 핵심 메시지
**Layout:** (1줄) 레이아웃 클래스
**Components:** (1줄) 사용할 컴포넌트 클래스 목록

**Content Zones:** (테이블)
**Zone 우선순위:** (1줄)

**Visual Design:** (테이블)
**시선 흐름 (Eye Path):** (2-3줄)
**강조 기법:** (1-2줄)

**Image/Icon:** (1-2줄)
**Animation:** (1-2줄)

**Text Draft:** (전체 텍스트)
**Speaker Notes:** (3-5줄)
**Flow Context:** (3줄)
```

---

## 2. Content Zones 설계 원칙

### 2.1 Zone 테이블 규칙

| Zone | 위치 | 요소 | 내용 | 밀도 |
|------|------|------|------|------|
| Z1 | 물리적 위치 | `tag.class` | 텍스트 요약 | 정량적 제한 |

- Zone ID: Z1부터 순서대로 (위치순, 시선 우선순위순 아님)
- 위치: `상단 전체폭`, `좌측`, `우측`, `하단`, `중앙`, `본문 전체폭` 등
- 요소: 구체적 HTML 태그 + CSS 클래스 (`h2.slide-heading`, `div.kpi-card`, `ul.slide-bullets`)
- 내용: Zone에 들어갈 텍스트 요약 (전문은 Text Draft에)
- 밀도: `1줄`, `3항목, 각 8단어 이내`, `5불릿`, `4 KPI 카드` 등 정량적

### 2.2 Zone 상한

- 한 슬라이드에 Zone 최대 **6개**
- Z1은 **항상 heading** — 슬라이드의 주장(assertion)을 완전한 문장으로
- 마지막 Zone은 강조 또는 요약 — 핵심 메시지를 반복하거나 CTA 배치
- 전체 밀도: **75단어**, **5불릿**, 불릿당 **10단어**

### 2.3 텍스트/비주얼 비율

| 슬라이드 유형 | 텍스트 : 비주얼 |
|-------------|-------------|
| 개념 설명 (text-image) | 50:50 |
| 데이터/KPI | 30:70 |
| 비교 (two-col) | 60:40 |
| 프로세스/타임라인 | 20:80 |
| 실습/실행 | 70:30 |
| 인용/강조 | 40:60 |
| 코드 쇼케이스 | 50:50 |

---

## 3. Visual Design 설계 원칙

### 3.1 Visual Design 테이블 규칙

| 요소 | 속성 | 값 | 이유 |
|------|------|------|------|
| 구체적 Zone/요소 | CSS 속성 | 디자인 토큰 | 판단 근거 |

- **모든 색상은 CSS 변수:** `--color-primary`, `--color-text-secondary` 등. hex 값 직접 사용 금지.
- **모든 크기는 디자인 토큰:** `--type-body`, `--space-4`, `--gap-md` 등.
- **"이유" 컬럼 필수:** 왜 이 값을 선택했는지 한 줄 설명.
- 배경, 여백, 그림자, 테두리, 간격을 **모두** 명시.
- 슬라이드별 특수 CSS가 필요하면 여기에 기재.

### 3.2 강조 규칙

- **슬라이드당 강조 포인트 1개만.** 색상 강조, 크기 강조, 위치 강조 중 택 1.
- 색상 사용: primary + secondary + text-primary + text-secondary **최대 4색**.
- 그림자/elevation: 카드형 컴포넌트에만. 텍스트 요소에는 사용 금지.
- 배경: 콘텐츠 슬라이드는 `--color-background`, 강조 슬라이드만 colored bg.

### 3.3 타이포 위계

heading(2rem) > subheading(1.5rem) > body(1.125rem) > caption(0.8125rem)

한 슬라이드에서 **최대 3단계**만 사용. 예: heading + body + caption은 OK. heading + subheading + body + caption은 너무 많음.

---

## 4. 시선 흐름 설계

### 4.1 패턴별 가이드

| 패턴 | 적용 대상 | 흐름 |
|------|---------|------|
| F-패턴 | 일반 콘텐츠 (text, text-image) | 좌상단 heading → 좌측 본문 → 우측 보조 |
| Z-패턴 | 비교/그리드 (two-col, kpi) | 좌상단 → 우상단 → 좌하단 → 우하단 |
| 중앙 집중 | 타이틀, 섹션 디바이더, 인용구 | 중앙에서 시작 → 바깥으로 확산 |
| 순차 | 프로세스, 타임라인 | 좌에서 우로 단계적 이동 |

### 4.2 시각적 무게 순서

크기 > 색상 > 위치(좌상단) > 그림자 > 테두리

가장 중요한 요소에 가장 강한 무게를 부여한다.

---

## 5. 레이아웃별 Zone 템플릿

각 레이아웃의 기본 Zone 구성. 스펙 작성 시 이 템플릿을 시작점으로 사용하고 슬라이드 내용에 맞게 조정.

### layout-title
```
Z1: 상단 — eyebrow (라벨)
Z2: 중앙 — title (메인 타이틀)
Z3: 중앙 — subtitle (부제)
Z4: 하단 — meta (발표자, 날짜)
```

### layout-section-divider
```
Z1: 중앙 — section-number (배경 워터마크)
Z2: 중앙 — section-title
Z3: 중앙 — section-description
```

### layout-text
```
Z1: 상단 — slide-heading
Z2: 상단 — slide-subheading (선택)
Z3: 본문 — 텍스트/불릿/컴포넌트
```

### layout-text-image
```
Z1: 좌측 상단 — eyebrow (선택)
Z2: 좌측 — slide-heading
Z3: 좌측 — body + bullets
Z4: 우측 — image/SVG
```

### layout-two-col
```
Z1: 상단 전체폭 — slide-heading
Z2: 좌측 라벨 — col-label
Z3: 좌측 카드 — col-card + 내용
Z4: 우측 라벨 — col-label
Z5: 우측 카드 — col-card + 내용
Z6: 하단 (선택) — 요약/강조 문장
```

### layout-three-col
```
Z1: 상단 — slide-heading + subheading
Z2: 좌측 카드 — feature-card
Z3: 중앙 카드 — feature-card
Z4: 우측 카드 — feature-card
```

### layout-kpi
```
Z1: 상단 — slide-heading + subheading
Z2: 본문 — kpi-grid (1x3, 1x4, 2x2, featured)
```

### layout-process
```
Z1: 상단 — slide-heading + subheading
Z2: 본문 — process-flow (step circles + arrows)
```

### layout-code
```
Z1: 상단 — slide-heading + subheading
Z2: 좌측 — code-pane (코드 블록)
Z3: 우측 — code-result-pane (결과/설명)
```

### layout-quote
```
Z1: 상단 중앙 — quote-mark
Z2: 중앙 — quote-text
Z3: 하단 중앙 — attribution (이름, 직책)
```

### layout-simple
```
Z1: 중앙 — icon (이모지)
Z2: 중앙 — title
Z3: 중앙 — description
```

### layout-before-after
```
Z1: 상단 전체폭 — slide-heading
Z2: 좌측 — before-pane (라벨 + 내용)
Z3: 우측 — after-pane (라벨 + 내용)
```

### layout-agenda
```
Z1: 상단 — slide-heading
Z2: 본문 — agenda-list (번호 + 제목 + 시간)
```

### layout-team / layout-pricing / layout-timeline
기본 패턴은 layout-kpi와 동일: Z1(heading) + Z2(grid 본문).

---

## 6. 전후 슬라이드 연결 규칙

### 6.1 레이아웃 다양성
- 같은 레이아웃 **3연속 금지** — 시각적 단조로움 방지
- 같은 세션 내에서 최소 4종 이상의 레이아웃 사용

### 6.2 밀도 교차
- 밀도 높은 슬라이드 (비교, KPI, 코드) 뒤에는 밀도 낮은 슬라이드 (실습, 섹션 디바이더) 배치
- 텍스트 3장 연속 후에는 비주얼 슬라이드 (이미지, 다이어그램, 프로세스) 삽입

### 6.3 색상 리듬
- 보라 배경 슬라이드 (섹션 디바이더, 타이틀) 사이에 최소 4장의 밝은 배경 슬라이드
- 연속 밝은 배경 슬라이드에서는 카드 그림자와 상단 악센트 라인으로 시각적 변화 부여

### 6.4 콘텐츠 흐름
- 이론 → 구조 → 실습 순서 유지 (개념 설명 → 프로세스/다이어그램 → 실습 안내)
- 실습 디브리프 뒤에는 다음 주제의 개념 슬라이드 또는 섹션 디바이더

---

## 7. Image/Icon 설계 규칙

### 7.1 이미지 필요 판단

| 슬라이드 유형 | 이미지 필요? | 권장 유형 |
|-------------|-----------|---------|
| 개념 설명 | 선택 | SVG 다이어그램 또는 아이콘 |
| 사례/데모 | 필수 | 스크린샷 SVG 또는 스톡 이미지 |
| 비교 | 불필요 | 텍스트로 충분 |
| KPI/데이터 | 불필요 | 숫자 자체가 비주얼 |
| 프로세스 | 불필요 | 프로세스 아이콘이 비주얼 역할 |
| 실습 | 불필요 | callout 컴포넌트로 충분 |

### 7.2 SVG 다이어그램 규칙
- `viewBox="0 0 400 300"`, `style="width:100%; min-height:200px;"`
- 팔레트 색상 hex 직접 사용 (#7C3AED, #06B6D4 등)
- 배경: `<rect rx="12" fill="..." opacity="0.08"/>`
- 폰트: `font-family="Sora, sans-serif"`
- 단순하고 의미 있는 도형: 원, 화살표, 사각형, 선

### 7.3 이모지 아이콘
- KPI 카드, 프로세스 스텝, 기능 카드에서 이모지를 아이콘으로 활용
- 슬라이드당 이모지 최대 5개
- 같은 의미의 이모지는 프레젠테이션 전체에서 일관되게 사용

---

## 8. Animation 설계 규칙

| 요소 유형 | fragment 사용 | 이유 |
|---------|-------------|------|
| 순서형 리스트 (icon-list, bullets) | `fragment fade-up` | 발표자가 하나씩 설명 |
| 그리드 컴포넌트 (KPI, feature-card) | 사용 금지 | 그리드는 전체가 보여야 비교 가능 |
| 비교 (two-col) | 사용 금지 | 좌우 동시 비교가 목적 |
| 코드 블록 | 사용 금지 | 코드는 전체 맥락이 필요 |
| 인용구 | 사용 금지 | 한 번에 읽어야 임팩트 |
| 프로세스 | 선택적 `fragment fade-up` | 단계별 설명 시에만 |

전환 효과:
- 섹션 디바이더: `data-transition="fade"`
- 나머지: 글로벌 transition 사용 (기본 `slide`)

---

## 9. Speaker Notes 작성 규칙

- 슬라이드에 적힌 내용을 반복하지 않음
- **보충 설명** (왜 이게 중요한지, 실제 사례, 데이터 출처)
- **전환 멘트** (다음 슬라이드로 넘어가는 브릿지 문장)
- **시간 가이드** (이 슬라이드에 할당된 시간)
- 길이: 3-5줄 (발표자가 한눈에 읽을 수 있는 분량)
