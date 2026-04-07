---
name: pptmaker
description: Use when creating presentations, pitch decks, slide decks, or any reveal.js-based HTML presentation. Triggers on "PPT 만들어", "프레젠테이션", "발표 자료", "pitch deck", "slide deck", "reveal.js presentation", or any request to create slides for a talk, meeting, or demo.
---

# reveal.js Presentation Generator

Generate professional reveal.js HTML presentations via a 4-phase pipeline. Each phase loads only the reference files it needs.

## Phase 1: Analysis

Parse the user's request and determine:
- **Presentation type:** investor pitch / internal (status, proposal, QBR) / conference (lightning, standard, workshop) / sales (PAS, showcase, case study) / educational (lecture, tutorial)
- **Audience, duration, tone**
- If information is missing, ask — but keep questions minimal

No files loaded. Use context clues to classify.

## Phase 2: Structuring

Read `references/pitch-structures.md`. Select the matching scenario structure. Design the slide outline (number, role, key message per slide).

**Present the outline to the user and wait for approval before proceeding.**

## Phase 3: Design Application

Read `references/design-system.md`, `templates/layouts.md`, `templates/components.md`.

Map each slide to a layout and component set. Select palette + font pairing based on tone:

| Tone | Palette | Font Pairing |
|------|---------|-------------|
| Corporate / Finance | Corporate (Navy) | Playfair Display + Source Sans 3 |
| Startup / Product | Startup (Violet) | Plus Jakarta Sans + DM Sans |
| Technical / Dev | Dark (Charcoal) | Inter |
| Consulting / Academic | Minimal (Teal) | Inter |
| Creative / Marketing | Creative (Coral) | Fraunces + Inter |
| Education / Friendly | Startup (Violet) | Sora + Nunito Sans |

## Phase 4: Generation

Read `templates/base.html`, `references/revealjs-api.md`.

1. Start from base.html boilerplate
2. Replace `{{FONT_LINKS}}` with selected Google Fonts `<link>` tags
3. Replace `{{DESIGN_TOKENS}}` with selected palette CSS variables + typography tokens
4. Replace `{{LAYOUT_CSS}}` with CSS for used layouts only
5. Replace `{{COMPONENT_CSS}}` with CSS for used components only
6. Build each `<section>` with mapped layout class, user content, and appropriate fragments/transitions
7. For image slots: WebSearch for relevant stock images (Unsplash/Pexels), embed URLs with `data-image-slot` and `data-image-desc` markers
8. Replace `{{TRANSITION}}` (default: `slide`)
9. Write final HTML file as `{topic-slug}-presentation.html`

## Phase 5: Quality Review (Automatic)

After Phase 4 completes, automatically launch parallel subagents to review and fix every slide. Do NOT skip this phase.

**Batch strategy:** Group slides by 10-15 per agent. For a 72-slide deck, dispatch 5-6 agents in parallel.

Each agent receives:
- The HTML file path
- Its assigned slide range (e.g., slides 1-12)
- The design system reference path
- The layouts/components reference paths

**Each agent must Read the HTML, then for each slide in its range check:**

1. **Layout correctness** — Does the `<section>` use the correct layout class? Are all required child elements present (e.g., `.title-eyebrow`, `.title-main` for layout-title)?
2. **Typography hierarchy** — Are heading sizes larger than body? Are labels using `--type-label`? No more than 3 font sizes per slide?
3. **Content density** — Max 75 words body text per slide, max 5 bullet points, max 10 words per bullet?
4. **Visual balance** — Does the slide have sufficient whitespace? Are elements aligned to the grid?
5. **Fragment usage** — Are fragments used purposefully (not on every element)?
6. **Color consistency** — All colors via `var()` tokens? No hardcoded colors except code backgrounds?
7. **Image slots** — Do image slots have `data-image-slot`, `data-image-desc`, and `alt` attributes?
8. **Accessibility** — Alt text present? Sufficient contrast? No color-only meaning?
9. **Speaker notes** — Do section dividers and exercise slides have `<aside class="notes">`?
10. **Korean text quality** — Natural phrasing? No truncated sentences? Proper spacing?

**Agent output:** For each issue found, the agent directly Edits the HTML file to fix it. If a fix requires judgment (e.g., restructuring content), the agent describes the issue and proposed fix in its output for human review.

**After all agents complete:** Report a summary table:

```
슬라이드 품질 검증 완료:
| 범위 | 검토 | 수정 | 주요 변경 |
|------|------|------|----------|
| 1-12 | 12  | 3    | 타이포 수정, fragment 추가 |
| ...  | ... | ...  | ...      |
```

## Image Management

After generation, if the user requests image changes:
1. Read the HTML file
2. List all `data-image-slot` markers with descriptions
3. Replace via user-provided URL or WebSearch with new keywords
