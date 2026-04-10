---
name: pptmaker
version: 0.2.0
description: Use when creating presentations, pitch decks, or slide decks. Generates a Gamma-optimized markdown prompt file to paste into gamma.app. Triggers on "PPT 만들어", "프레젠테이션", "발표 자료", "pitch deck", "slide deck", or any request to create slides for a talk, meeting, or demo.
---

# Gamma Presentation Prompt Generator

Generate a Gamma-optimized markdown file via a 4-phase pipeline. The output is a `.md` file ready to paste into [Gamma](https://gamma.app) for high-quality presentation generation.

**Output deliverables:**
1. `{topic}-gamma-prompt.md` — Gamma에 붙여넣을 최종 프롬프트
2. `{topic}-speaker-notes.md` — 슬라이드별 발표자 노트 (별도 파일)

---

## Phase 1: Analysis

Parse the user's request and determine:
- **Presentation type:** investor pitch / internal (status, proposal, QBR) / conference (lightning, standard, workshop) / sales (PAS, showcase, case study) / educational (lecture, tutorial)
- **Audience, duration, tone**
- **Slide count target** (Gamma는 한 번에 최대 30장 생성)
- If information is missing, ask — but keep questions minimal

No files loaded. Use context clues to classify.

---

## Phase 2: Structuring

Read `references/pitch-structures.md`. Select the matching scenario structure. Design the slide outline (number, role, key message per slide).

**Present the outline to the user and wait for approval before proceeding.**

---

## Phase 3: Content Design Spec

After the outline is approved, create a detailed content spec for every slide.

1. Read `references/slide-design-guide.md` — **콘텐츠 설계 원칙만 추출**. HTML/CSS/레이아웃 클래스 관련 내용은 무시.
2. For each slide in the approved outline, write a content spec block:

```
### Slide N: {제목}

**Role:** 이 슬라이드의 역할과 핵심 메시지 (1줄)
**Visual Type:** 비주얼 유형 — 텍스트, 비교, 카드 그리드, 차트, 타임라인, 인용구, 이미지+텍스트 등
**Density:** 불릿 수, 단어 수 등 정량적 제한

**Text Draft:**
- 제목: ...
- 부제/소제목: ... (선택)
- 본문: 불릿 또는 짧은 단락
- 강조 텍스트: ... (선택)

**Image Suggestion:** Gamma AI가 생성할 이미지 설명 (SPLICE 형식 권장)
- Setting(배경) / People(인물) / Lighting(조명) / Immediacy(분위기) / Composition(구도) / Execution(스타일)
- 차트/그래프인 경우: 차트 유형 + 데이터 명시

**Speaker Notes:** (3-5줄)
- 슬라이드 텍스트를 반복하지 않음
- 보충 설명, 실제 사례, 데이터 출처
- 전환 멘트 (다음 슬라이드로의 브릿지)
- 시간 가이드

**Flow Context:**
- 이전 슬라이드와의 연결: ...
- 다음 슬라이드로의 전환: ...
```

3. Write the complete spec to `{topic}-slide-specs.md`
4. **Present the spec file to the user for review before proceeding.**

### Content Design Principles

Phase 3에서 적용할 핵심 원칙 (slide-design-guide.md에서 발췌):

- **슬라이드당 핵심 메시지 1개** — 여러 메시지를 섞지 않음
- **밀도 상한:** 75단어, 6불릿 이내, 불릿당 30단어 이내
- **같은 비주얼 유형 3연속 금지** — 텍스트→차트→카드→비교 등 다양하게
- **밀도 교차:** 데이터 슬라이드 뒤에는 가벼운 슬라이드 배치
- **강조 포인트 1개:** 색상/크기/위치 강조 중 택 1
- **이론 → 구조 → 실습 순서 유지**

---

## Phase 4: Gamma Prompt Export

Approved spec을 Gamma에 붙여넣을 수 있는 깨끗한 마크다운 파일로 변환.

Read `references/gamma-guide.md` for Gamma-specific formatting rules.

### Step 1: Extract & Transform

`{topic}-slide-specs.md`에서 순수 콘텐츠만 추출:

1. **파일 첫 줄 = 타이틀 슬라이드 시작** — 프론트매터, 메타데이터, 문서 제목 없이 바로 첫 슬라이드
2. **`---`로 슬라이드 구분** — 각 슬라이드/카드 사이에 `---` 삽입
3. **Text Draft만 추출** — Role, Visual Type, Density, Flow Context 등 스펙 라벨 모두 제거
4. **Speaker Notes 분리** — `{topic}-speaker-notes.md`로 별도 저장

### Step 2: Gamma Optimization

추출된 마크다운에 다음 보정 적용:

#### 구조 규칙
- **`#` = 타이틀 슬라이드 제목** (파일에서 1회만 사용)
- **`##` = 슬라이드 제목** — 각 카드의 주 제목
- **`###` = 카드 내 하위 섹션** — 한 카드 내에서 구분이 필요할 때만
- **불릿은 `-`로 통일** — `*`, `+`, 숫자 리스트와 혼용 금지
- **빈 줄로 요소 구분** — 제목과 본문, 불릿 그룹 사이에 빈 줄

#### 콘텐츠 밀도
- **카드당 불릿 ≤ 6개, 불릿당 ≤ 30단어**
- **한 카드 = 하나의 핵심 메시지**
- **빈 카드 없음** — 모든 카드에 최소 제목 + 2-3개 콘텐츠 요소
- **긴 단락 → 불릿으로 변환** — Gamma는 구조화된 짧은 콘텐츠를 더 잘 해석

#### 제거 대상
- YAML frontmatter (`---` 사이의 메타데이터 블록)
- 스펙 라벨 (`**Role:**`, `**Visual Type:**`, `**Density:**`, `**Flow Context:**`)
- 마크다운 테이블 (Gamma가 자체 생성하므로 비교 내용은 불릿/서술로 전환)
- HTML 태그, CSS 클래스, 코드 블록 (프레젠테이션 콘텐츠가 아닌 경우)
- 문서 서식 요소 (목차, 페이지 번호, 헤더/푸터)

#### 이미지 힌트
이미지가 필요한 슬라이드에 blockquote 형식으로 삽입:

```markdown
> Image: 다양한 인종의 팀원들이 화이트보드 앞에서 브레인스토밍하는 밝은 오피스 환경, 따뜻한 자연광, 모던한 인테리어
```

차트/그래프가 필요한 경우:

```markdown
> Chart: 2023-2026 매출 성장 추이 (막대 차트)
> 2023: 50억 / 2024: 80억 / 2025: 120억 / 2026E: 180억
```

#### 한국어 최적화
- **문장은 짧고 명확하게** — 한 불릿에 2줄 이상 금지
- **한자어/영문 혼용 시 띄어쓰기 통일** — `AI 기반`, `SaaS 플랫폼` 형식
- **핵심 키워드 볼드 처리** — `**핵심 수치**`, `**차별점**` 등
- **50자 이상의 긴 문장은 분할** — 가독성 우선

#### 비교/대조 콘텐츠 처리
테이블 대신 Gamma가 자동으로 비교 카드를 생성할 수 있도록 구조화:

```markdown
## 기존 방식 vs 새로운 방식

**기존 방식**
- 수동 프로세스, 주 40시간 소요
- 오류율 15%
- 확장 불가

**새로운 방식**
- 자동화, 주 4시간으로 단축
- 오류율 0.1%
- 무제한 확장
```

### Step 3: Output

1. `{topic}-gamma-prompt.md` 작성 — Gamma에 붙여넣을 최종 파일
2. `{topic}-speaker-notes.md` 작성 — 슬라이드 번호별 발표자 노트

사용자에게 안내 메시지 출력:

```
Gamma 프롬프트 파일이 생성되었습니다.

사용법:
1. gamma.app 접속 → "Create new" → "Paste in text"
2. {topic}-gamma-prompt.md 내용을 전체 복사하여 붙여넣기
3. 테마/스타일 선택 후 "Generate"
4. 생성 후 {topic}-speaker-notes.md를 참고하여 각 카드에 speaker notes 수동 추가

팁:
- 생성 후 각 카드의 "Enhance" 버튼으로 디자인 품질 향상 가능
- 이미지가 마음에 들지 않으면 개별 카드에서 AI 이미지 재생성
- 최종 배포는 PDF로 내보내기 권장 (PPTX는 레이아웃이 깨질 수 있음)
- 워크스페이스 테마를 미리 설정하면 브랜드 일관성 유지 가능
```

---

## Output Format Example

최종 `{topic}-gamma-prompt.md` 파일의 구조:

```markdown
# 프레젠테이션 제목
부제목 — 발표자명 · 날짜

---

## 핵심 문제 정의

- **현재 상황**: 시장이 급변하고 있으나 기존 도구로는 대응 불가
- **핵심 과제**: 의사결정 속도를 3배 향상해야 함
- 고객의 78%가 더 빠른 응답을 기대

> Image: 복잡한 데이터 대시보드를 바라보며 고민하는 비즈니스 전문가, 모던한 사무실 배경

---

## 우리의 솔루션

AI 기반 실시간 분석 플랫폼

- **자동 인사이트 추출**: 데이터에서 패턴을 자동 감지
- **실시간 알림**: 중요 변화 발생 시 즉시 통보
- **원클릭 리포트**: 경영진 보고서를 1분 만에 생성

---

## 시장 기회

> Chart: TAM/SAM/SOM (동심원 차트)
> TAM: 500억 / SAM: 120억 / SOM: 30억 (2026 기준)

- 글로벌 비즈니스 인텔리전스 시장 **연 12% 성장**
- 국내 AI 분석 도구 도입률 아직 23%로 초기 단계
- 3년 내 시장 규모 2배 성장 전망
```
