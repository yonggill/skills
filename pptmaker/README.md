# pptmaker — reveal.js Presentation Generator

Generate professional reveal.js HTML presentations from natural language descriptions. Outputs a single CDN-based HTML file that opens in any browser — no local install needed.

## Usage

```
/pptmaker                  # Start the presentation workflow
/pptmaker 투자 피칭 덱 만들어줘, 시리즈A, 20분
```

Or say "PPT 만들어줘", "발표 자료", "pitch deck", "프레젠테이션" in natural language.

## How It Works

### Phase 1: Analysis

Parses the user's request to determine:

| Factor | Options |
|--------|---------|
| Type | Investor pitch / Internal (status, proposal, QBR) / Conference (lightning, standard, workshop) / Sales (PAS, showcase, case study) / Educational (lecture, tutorial) |
| Audience | Investors, executives, engineers, students, etc. |
| Duration | 5 min ~ 3 hours |
| Tone | Corporate, startup, technical, creative, educational |

Asks minimal follow-up questions if information is missing.

### Phase 2: Structuring

Loads `references/pitch-structures.md` and selects the matching scenario framework:

- **Investor pitch** — Kawasaki 10/20/30, Sequoia, YC formats
- **Internal** — BLUF + RAG, ADR-based proposals, QBR
- **Conference** — Lightning (5min), standard (30min), workshop (60-180min)
- **Sales** — Problem-Agitation-Solution, feature showcase, case study
- **Educational** — Lecture, tutorial, hands-on workshop

Presents the slide outline to the user for approval before proceeding.

### Phase 3: Design Application

Loads `references/design-system.md`, `templates/layouts.md`, `templates/components.md`.

Maps each slide to a layout + component set and selects palette + font:

| Tone | Palette | Font Pairing |
|------|---------|-------------|
| Corporate / Finance | Navy | Playfair Display + Source Sans 3 |
| Startup / Product | Violet | Plus Jakarta Sans + DM Sans |
| Technical / Dev | Dark Charcoal | Inter |
| Consulting / Academic | Minimal Teal | Inter |
| Creative / Marketing | Coral | Fraunces + Inter |
| Education / Friendly | Violet | Sora + Nunito Sans |

### Phase 4: Generation

Assembles the final HTML from `templates/base.html`:

1. Google Fonts CDN links
2. Design system CSS tokens (palette + typography + spacing)
3. Layout CSS for used layouts only
4. Component CSS for used components only
5. Slide `<section>` elements with content, fragments, transitions
6. Stock images via WebSearch (Unsplash/Pexels) with `data-image-slot` markers
7. reveal.js initialization with plugins

### Phase 5: Quality Review (Automatic)

Dispatches parallel subagents (10-15 slides per agent) to review every slide:

- Layout correctness and required child elements
- Typography hierarchy (max 3 font sizes/slide)
- Content density (max 75 words, 5 bullets, 10 words/bullet)
- Color consistency (all via `var()` tokens)
- Accessibility (alt text, WCAG contrast)
- Speaker notes on section dividers and exercises
- Korean text quality

Issues are fixed directly in the HTML file.

## Design System

### 5 Color Palettes

| Name | Primary | Best For |
|------|---------|---------|
| Corporate (Navy) | `#1B3A6B` | Finance, enterprise, B2B |
| Startup (Violet) | `#7C3AED` | Product launches, pitches |
| Minimal (Teal) | `#18181B` + `#0D9488` | Research, consulting |
| Creative (Coral) | `#EA580C` | Marketing, design |
| Dark (Charcoal) | `#38BDF8` on `#0F172A` | Dev talks, tech demos |

### 15 Slide Layouts

Title, Section Divider, Text+Image, Two-Column, Three-Column, Full-Image Overlay, Quote, KPI Dashboard (4 grid variants), Timeline (horizontal/vertical), Process Flow, Code Showcase, Team Grid, Pricing Table, Before/After, Agenda/TOC.

### 9 Reusable Components

KPI Card, Feature Card, Quote Block, Image+Caption, Numbered List, Progress Bar, Badge/Tag, Callout Box, Icon Grid.

## Image Management

Images are automatically sourced from stock photo sites during generation. Each image has a slot marker:

```html
<img src="..." data-image-slot="3" data-image-desc="팀 브레인스토밍 장면" />
```

After generation, request changes:
- "슬라이드 5 이미지 바꿔줘" — search for replacement
- Provide a URL directly — swap instantly

## Output

A single `.html` file (typically 2,000-4,000 lines). Open in any modern browser.

- Arrow keys to navigate
- `S` for speaker notes view
- `ESC` for slide overview
- `?` for keyboard shortcuts

## Installation

Copy the `pptmaker/` directory to `~/.claude/skills/`:

```
~/.claude/skills/pptmaker/
  SKILL.md
  references/
    revealjs-api.md
    pitch-structures.md
    design-system.md
  templates/
    layouts.md
    components.md
    base.html
```

## File Sizes

| File | Lines | Role |
|------|-------|------|
| SKILL.md | ~100 | Workflow logic |
| revealjs-api.md | ~1,700 | reveal.js technical reference |
| pitch-structures.md | ~1,100 | Presentation theory + scenarios |
| design-system.md | ~750 | Colors, typography, spacing |
| layouts.md | ~1,900 | 15 layout HTML/CSS |
| components.md | ~750 | 9 component HTML/CSS |
| base.html | ~70 | HTML boilerplate |

## Notes

- **CDN-based.** Requires internet connection. Uses unpkg (reveal.js 4.6.1) and Google Fonts.
- **Korean-first.** All templates and examples optimized for Korean text. Works with any language.
- **No image generation.** Uses stock image search + placeholder system. Swap images after generation.
