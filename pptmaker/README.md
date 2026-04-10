# pptmaker — Gamma Presentation Prompt Generator

Generate a Gamma-optimized markdown file from natural language descriptions. Outputs a `.md` file ready to paste into [gamma.app](https://gamma.app) for high-quality presentation generation.

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
| Slide count | Target (max 30 per Gamma generation) |

### Phase 2: Structuring

Loads `references/pitch-structures.md` and selects the matching scenario framework. Presents the slide outline to the user for approval.

### Phase 3: Content Design Spec

Creates a detailed content spec for every slide with:
- Role & key message
- Visual type (text, comparison, card grid, chart, timeline, quote, etc.)
- Text Draft (actual slide content)
- Image suggestions (SPLICE format for Gamma AI image generation)
- Speaker notes
- Flow context (slide-to-slide transitions)

Writes spec to `{topic}-slide-specs.md` for user review.

### Phase 4: Gamma Prompt Export

Transforms the approved spec into a clean markdown file optimized for Gamma:
- `---` separators between slides
- First section = title slide (no preamble)
- Bullets and headings only (no tables, no HTML)
- Image hints as blockquotes (`> Image: ...`)
- Chart hints with data (`> Chart: ...`)
- Korean text optimized (short sentences, bold keywords)

## Output

Two files:

1. **`{topic}-gamma-prompt.md`** — Paste into Gamma's "Paste in text" to generate
2. **`{topic}-speaker-notes.md`** — Slide-by-slide speaker notes (add manually in Gamma)

## Gamma Tips

- Apply workspace theme before generating for brand consistency
- Use "Enhance" on individual cards to improve design
- Export as PDF (PPTX may have layout shifts)
- Gamma generates up to 30 slides at once; add more manually after

## Installation

```
~/.claude/skills/pptmaker/
  SKILL.md
  README.md
  references/
    pitch-structures.md
    slide-design-guide.md
    gamma-guide.md
```

## Notes

- **Korean-first.** All templates and examples optimized for Korean text. Works with any language.
- **Design is Gamma's job.** This skill focuses on content structure and narrative quality. Gamma handles layout, colors, typography, and images.
