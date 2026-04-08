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

## Phase 2.5: Slide Design Spec

After the outline is approved, create a detailed design spec for every slide.

1. Read `references/slide-design-guide.md`
2. For each slide in the approved outline, write a full spec block following the guide's format:
   - Role, Layout, Components
   - Content Zones table (position, element, content, density)
   - Visual Design table (element, property, token value, rationale)
   - Eye path, emphasis technique
   - Image/Icon plan, Animation plan
   - Text Draft (actual text for every zone)
   - Speaker Notes
   - Flow Context (previous/next slide connection)
3. Write the complete spec to `{topic}-slide-specs.md` in the same directory as the presentation
4. **Present the spec file to the user for review before proceeding.**

Select palette + font pairing based on tone (applies to all specs):

| Tone | Palette | Font Pairing |
|------|---------|-------------|
| Corporate / Finance | Corporate (Navy) | Playfair Display + Source Sans 3 |
| Startup / Product | Startup (Violet) | Plus Jakarta Sans + DM Sans |
| Technical / Dev | Dark (Charcoal) | Inter |
| Consulting / Academic | Minimal (Teal) | Inter |
| Creative / Marketing | Creative (Coral) | Fraunces + Inter |
| Education / Friendly | Startup (Violet) | Sora + Nunito Sans |

## Phase 3: Assembly (Spec → HTML)

Phase 3 does NOT make design decisions. It mechanically assembles HTML from the approved slide specs.

Read `{topic}-slide-specs.md`, `references/design-system.md`, `templates/layouts.md`, `templates/components.md`.

For each slide spec:
1. Apply the specified Layout class to `<section>`
2. Build Content Zones as specified (exact HTML elements, classes, content)
3. Apply Visual Design table values as CSS (inline or via existing classes)
4. Insert Text Draft content verbatim
5. Add Speaker Notes as `<aside class="notes">`
6. Apply Animation directives as fragment classes

## Phase 4: Generation

**Before generating, read the Generation Rules section below. Every rule is mandatory.**

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

## Generation Rules (MANDATORY)

These rules apply during Phase 4. Violating them causes layout breaks.

### reveal.js Compatibility
- Set `center: false` in Reveal.initialize — all centering is handled by layout CSS
- Every `<section>` gets its full-height layout class — no bare sections
- Never set `height: 100%` on any layout class — the global override handles it
- Never use inline `style="display: grid"` or `style="display: flex"` — use layout classes only

### Overflow Prevention
- Every grid/flex child must have `min-width: 0`
- Grid gaps: max `1rem` for 3+ columns, max `1.5rem` for 2 columns
- Total content width (padding + gaps + content) must not exceed 1280px
- Use `overflow: hidden` on all containers with constrained children

### Typography for Projection
- Minimum body text: `var(--type-body)` (1.125rem / 18px) — never smaller for body
- Minimum readable text: `var(--type-body-sm)` (1rem / 16px) — for bullets and secondary
- Captions/labels only: `var(--type-caption)` (0.8125rem) — never for readable content
- Maximum 50 Korean characters per line — add line breaks or reduce text

### Heading Alignment Consistency
- Content slides: ALL headings left-aligned
- Title slide + Section dividers: centered
- Never mix alignment within a session

### Image Handling
- Use WebSearch to find real Unsplash/Pexels URLs — never use placehold.co for final output
- If WebSearch fails, use a CSS gradient background instead of a placeholder image:
  `background: linear-gradient(135deg, var(--color-primary), var(--color-secondary));`
- All images: `data-image-slot`, `data-image-desc`, `alt` attributes required
- placehold.co URLs must use ASCII-only text (Korean characters render as broken boxes)

### Animation Guidelines
- Use `fragment fade-up` on list items (icon-list, bullets) — max 5 items
- Do NOT use fragment on KPI cards, feature cards, or any grid-based component
- Section dividers: `data-transition="fade"`
- Content slides: use global transition (default: `slide`)

### Korean Text Rules
- `word-break: keep-all` is set globally — do not override with `break-all`
- For text inside `max-width` containers: always add `margin: 0 auto` for centering
- Avoid sentences longer than 2 lines at projection size — split into bullets

### Slide Density Balance
- Every content slide should use 60-80% of the vertical space
- If content is sparse (< 40% filled), add a supporting visual or split with previous slide
- If content overflows, split into 2 slides — never rely on overflow:hidden to clip content

## Phase 5: Visual Quality Review (Playwright-based, Automatic)

After Phase 4 completes, verify every slide by **rendering it in a real browser and examining screenshots**. Code-only review cannot catch layout breaks, text overflow, alignment issues, or visual imbalance. Do NOT skip this phase.

### Step 1: Capture Screenshots

Start a local HTTP server and use Playwright to screenshot every slide:

```javascript
// 1. Start server
// Run: python3 -m http.server 8765 (in the directory containing the HTML file)

// 2. Capture all slides via Playwright browser_run_code
async (page) => {
  await page.goto('http://localhost:8765/{filename}.html');
  await page.waitForTimeout(2000);
  const total = await page.evaluate(() => Reveal.getTotalSlides());
  for (let i = 0; i < total; i++) {
    await page.evaluate((idx) => Reveal.slide(idx), i);
    await page.waitForTimeout(300);
    await page.screenshot({
      path: `ppt-review-screenshots/slide-${String(i+1).padStart(2,'0')}.png`
    });
  }
}
```

Set viewport to `1280x720` before capturing. Save screenshots to a `ppt-review-screenshots/` directory.

### Step 2: Visual Review with Parallel Agents

Dispatch parallel subagents (15-18 slides per agent). Each agent receives:
- Screenshot file paths for its range
- The HTML file path
- Design system + layout reference paths

**Each agent must READ each screenshot PNG file (Claude is multimodal) and check:**

1. **Text overflow/cutoff** — Any text running off the slide edge or clipped by a container?
2. **Alignment** — Elements centered when they should be? Columns equal width? Grid items aligned?
3. **Spacing/cramping** — Enough breathing room? Elements too close together or too spread out?
4. **Readability** — Text large enough for a projected screen? Contrast sufficient?
5. **Layout integrity** — Grid/flex layouts rendering correctly? Overlapping elements?
6. **Korean text wrapping** — Words breaking mid-syllable? Awkward line breaks in constrained-width elements?
7. **Font rendering** — Correct fonts loading? Any fallback to system serif/sans?
8. **Color harmony** — Colors matching the selected palette? Any jarring or unintended colors?
9. **Component rendering** — Cards, KPI grids, timelines, process flows displaying as designed?
10. **Professional polish** — Would this look good projected on a screen in front of 50 people?

**For each visual issue:** The agent reads the HTML, locates the corresponding slide `<section>`, and Edits it to fix the problem. Common fixes:
- Add `word-break: keep-all` for Korean text wrapping
- Adjust `max-width` or shorten text for overflow
- Remove conflicting inline styles
- Add missing `margin: 0 auto` on centered elements with `max-width`
- Fix layout class mismatches

### Step 3: Re-capture and Verify (if fixes were made)

After agents complete, if fixes were applied:
1. Re-run Playwright to screenshot only the fixed slides
2. Read the new screenshots to confirm issues are resolved
3. If issues persist, fix and re-verify (max 2 iterations)

### Step 4: Report

```
슬라이드 시각 검증 완료:
| 범위 | 검토 | 이슈 | 수정 | 주요 변경 |
|------|------|------|------|----------|
| 1-18 | 18  | 3    | 3    | 텍스트 오버플로 수정, 정렬 보정 |
| ...  | ... | ...  | ...  | ...      |
```

Kill the HTTP server after review is complete.

## Phase 6: PDF Export (Automatic)

After Phase 5 completes, automatically generate a PDF version using decktape.

```bash
npx decktape reveal http://localhost:8765/{filename}.html {filename}.pdf \
  --size 1280x720 \
  --pdf-title "{presentation title}" \
  --pdf-author "{author}"
```

This produces a high-quality PDF with one page per slide, matching the browser rendering exactly. The PDF is saved alongside the HTML file.

Kill the HTTP server after PDF export is complete.

## Image Management

After generation, if the user requests image changes:
1. Read the HTML file
2. List all `data-image-slot` markers with descriptions
3. Replace via user-provided URL or WebSearch with new keywords
