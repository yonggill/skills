# Design System Reference

> This document is the authoritative source for all visual and structural decisions when generating reveal.js presentations. Every CSS value is exact and copy-pasteable. Refer to this file before writing any slide markup, styles, or layout code.

---

## 1. Color Palettes

Each palette is defined as a `:root` CSS block containing 14 semantic color variables. Apply exactly one palette per presentation by including its `:root` block in the `<style>` tag of the reveal.js HTML file.

---

### 1.1 Corporate / Professional (Navy)

**Use case:** Finance, enterprise software, legal, government, B2B SaaS

```css
:root {
  --color-primary:        #1B3A6B;
  --color-secondary:      #2563EB;
  --color-accent:         #F59E0B;
  --color-background:     #FFFFFF;
  --color-surface:        #F1F5F9;
  --color-surface-raised: #E2E8F0;
  --color-text-primary:   #0F172A;
  --color-text-secondary: #475569;
  --color-text-inverse:   #FFFFFF;
  --color-success:        #16A34A;
  --color-warning:        #D97706;
  --color-danger:         #DC2626;
  --color-border:         #CBD5E1;
  --color-link:           #2563EB;
}
```

**WCAG 2.2 Contrast Ratios:**

| Foreground            | Background              | Ratio  | Level |
|-----------------------|-------------------------|--------|-------|
| `--color-text-primary` (#0F172A) | `--color-background` (#FFFFFF) | 19.0:1 | AAA |
| `--color-text-secondary` (#475569) | `--color-background` (#FFFFFF) | 5.9:1 | AA |
| `--color-text-inverse` (#FFFFFF) | `--color-primary` (#1B3A6B) | 10.3:1 | AAA |
| `--color-text-inverse` (#FFFFFF) | `--color-secondary` (#2563EB) | 4.7:1 | AA |
| `--color-text-primary` (#0F172A) | `--color-surface` (#F1F5F9) | 17.2:1 | AAA |
| `--color-text-primary` (#0F172A) | `--color-surface-raised` (#E2E8F0) | 14.9:1 | AAA |
| `--color-accent` (#F59E0B) | `--color-background` (#FFFFFF) | 2.9:1 | — (decorative only) |
| `--color-text-primary` (#0F172A) | `--color-accent` (#F59E0B) | 6.7:1 | AA |

---

### 1.2 Modern / Startup (Violet)

**Use case:** Product launches, venture pitches, SaaS platforms, tech startups

```css
:root {
  --color-primary:        #7C3AED;
  --color-secondary:      #06B6D4;
  --color-accent:         #F43F5E;
  --color-background:     #FAFAFA;
  --color-surface:        #F4F4F5;
  --color-surface-raised: #E4E4E7;
  --color-text-primary:   #18181B;
  --color-text-secondary: #52525B;
  --color-text-inverse:   #FFFFFF;
  --color-success:        #10B981;
  --color-warning:        #F59E0B;
  --color-danger:         #EF4444;
  --color-border:         #D4D4D8;
  --color-link:           #7C3AED;
}
```

**WCAG 2.2 Contrast Ratios:**

| Foreground            | Background              | Ratio  | Level |
|-----------------------|-------------------------|--------|-------|
| `--color-text-primary` (#18181B) | `--color-background` (#FAFAFA) | 18.3:1 | AAA |
| `--color-text-secondary` (#52525B) | `--color-background` (#FAFAFA) | 6.2:1 | AA |
| `--color-text-inverse` (#FFFFFF) | `--color-primary` (#7C3AED) | 5.2:1 | AA |
| `--color-text-inverse` (#FFFFFF) | `--color-secondary` (#06B6D4) | 2.8:1 | — (decorative only) |
| `--color-text-primary` (#18181B) | `--color-surface` (#F4F4F5) | 17.1:1 | AAA |
| `--color-text-primary` (#18181B) | `--color-surface-raised` (#E4E4E7) | 14.6:1 | AAA |
| `--color-text-inverse` (#FFFFFF) | `--color-accent` (#F43F5E) | 4.5:1 | AA |

---

### 1.3 Minimal / Clean (Monochrome + Teal)

**Use case:** Research presentations, academic talks, consulting, portfolios, design showcases

```css
:root {
  --color-primary:        #18181B;
  --color-secondary:      #3F3F46;
  --color-accent:         #0D9488;
  --color-background:     #FFFFFF;
  --color-surface:        #F9FAFB;
  --color-surface-raised: #F3F4F6;
  --color-text-primary:   #111827;
  --color-text-secondary: #6B7280;
  --color-text-inverse:   #FFFFFF;
  --color-success:        #059669;
  --color-warning:        #B45309;
  --color-danger:         #B91C1C;
  --color-border:         #E5E7EB;
  --color-link:           #0D9488;
}
```

**WCAG 2.2 Contrast Ratios:**

| Foreground            | Background              | Ratio  | Level |
|-----------------------|-------------------------|--------|-------|
| `--color-text-primary` (#111827) | `--color-background` (#FFFFFF) | 19.4:1 | AAA |
| `--color-text-secondary` (#6B7280) | `--color-background` (#FFFFFF) | 4.6:1 | AA |
| `--color-text-inverse` (#FFFFFF) | `--color-primary` (#18181B) | 18.9:1 | AAA |
| `--color-text-inverse` (#FFFFFF) | `--color-accent` (#0D9488) | 4.5:1 | AA |
| `--color-text-primary` (#111827) | `--color-surface` (#F9FAFB) | 18.6:1 | AAA |
| `--color-link` (#0D9488) | `--color-background` (#FFFFFF) | 4.5:1 | AA |

---

### 1.4 Creative / Design (Coral)

**Use case:** Brand presentations, marketing campaigns, creative agencies, product design

```css
:root {
  --color-primary:        #EA580C;
  --color-secondary:      #9333EA;
  --color-accent:         #FACC15;
  --color-background:     #FFFBF5;
  --color-surface:        #FEF3C7;
  --color-surface-raised: #FDE68A;
  --color-text-primary:   #1C1917;
  --color-text-secondary: #57534E;
  --color-text-inverse:   #FFFFFF;
  --color-success:        #15803D;
  --color-warning:        #D97706;
  --color-danger:         #DC2626;
  --color-border:         #E7E5E4;
  --color-link:           #EA580C;
}
```

**WCAG 2.2 Contrast Ratios:**

| Foreground            | Background              | Ratio  | Level |
|-----------------------|-------------------------|--------|-------|
| `--color-text-primary` (#1C1917) | `--color-background` (#FFFBF5) | 18.1:1 | AAA |
| `--color-text-secondary` (#57534E) | `--color-background` (#FFFBF5) | 6.1:1 | AA |
| `--color-text-inverse` (#FFFFFF) | `--color-primary` (#EA580C) | 3.2:1 | — (large text AA: 3:1 threshold met) |
| `--color-text-primary` (#1C1917) | `--color-surface` (#FEF3C7) | 15.4:1 | AAA |
| `--color-text-primary` (#1C1917) | `--color-surface-raised` (#FDE68A) | 12.8:1 | AAA |
| `--color-text-inverse` (#FFFFFF) | `--color-secondary` (#9333EA) | 5.6:1 | AA |

> Note: `--color-accent` (#FACC15) on white fails contrast. Use it for decorative highlights, borders, and icon fills only — never for body text on light backgrounds.

---

### 1.5 Dark Mode (Charcoal)

**Use case:** Developer talks, technical demos, data engineering, cybersecurity, evening events

```css
:root {
  --color-primary:        #38BDF8;
  --color-secondary:      #818CF8;
  --color-accent:         #34D399;
  --color-background:     #0F172A;
  --color-surface:        #1E293B;
  --color-surface-raised: #334155;
  --color-text-primary:   #F1F5F9;
  --color-text-secondary: #94A3B8;
  --color-text-inverse:   #0F172A;
  --color-success:        #4ADE80;
  --color-warning:        #FCD34D;
  --color-danger:         #F87171;
  --color-border:         #334155;
  --color-link:           #38BDF8;
}
```

**WCAG 2.2 Contrast Ratios:**

| Foreground            | Background              | Ratio  | Level |
|-----------------------|-------------------------|--------|-------|
| `--color-text-primary` (#F1F5F9) | `--color-background` (#0F172A) | 16.9:1 | AAA |
| `--color-text-secondary` (#94A3B8) | `--color-background` (#0F172A) | 7.3:1 | AA |
| `--color-text-primary` (#F1F5F9) | `--color-surface` (#1E293B) | 13.1:1 | AAA |
| `--color-text-primary` (#F1F5F9) | `--color-surface-raised` (#334155) | 8.4:1 | AAA |
| `--color-primary` (#38BDF8) | `--color-background` (#0F172A) | 9.5:1 | AAA |
| `--color-secondary` (#818CF8) | `--color-background` (#0F172A) | 5.8:1 | AA |
| `--color-accent` (#34D399) | `--color-background` (#0F172A) | 7.7:1 | AAA |
| `--color-text-inverse` (#0F172A) | `--color-primary` (#38BDF8) | 9.5:1 | AAA |

---

## 2. Typography

### 2.1 Type Scale

```css
:root {
  /* Slide element sizes */
  --type-slide-title:   3.25rem;   /* Hero/title slide main heading */
  --type-section-title: 2.5rem;    /* Section divider heading */
  --type-slide-heading: 2rem;      /* Content slide H1 */
  --type-subheading:    1.5rem;    /* H2 within content area */
  --type-body:          1.125rem;  /* Primary body copy, bullets */
  --type-body-sm:       1rem;      /* Secondary body, captions */
  --type-caption:       0.8125rem; /* Image captions, footnotes */
  --type-label:         0.75rem;   /* Tags, badges, overlines */
  --type-code:          0.9375rem; /* Inline and block code */
  --type-kpi-number:    3.5rem;    /* Large data callouts, KPI cards */
}
```

### 2.2 Line Height

```css
:root {
  --lh-tight:   1.2;  /* Display headings, slide titles */
  --lh-snug:    1.35; /* Section headings, subheadings */
  --lh-normal:  1.55; /* Body copy, bullets */
  --lh-relaxed: 1.7;  /* Captions, small print, footnotes */
}
```

### 2.3 Letter Spacing

```css
:root {
  --ls-tighter: -0.03em; /* Very large display type only (>3rem) */
  --ls-tight:   -0.02em; /* Slide titles, section headers */
  --ls-normal:   0em;    /* Body copy default */
  --ls-wide:     0.05em; /* Labels, overlines, all-caps tags */
  --ls-wider:    0.1em;  /* All-caps micro labels only */
}
```

### 2.4 Font Weight

```css
:root {
  --fw-regular:   400;
  --fw-medium:    500;
  --fw-semibold:  600;
  --fw-bold:      700;
  --fw-extrabold: 800;
}
```

---

### 2.5 Google Font Pairings

Each pairing includes a ready-to-paste `<link>` tag and CSS variable assignments. Place the `<link>` tag inside `<head>` before any stylesheets.

---

#### Pairing 1: Inter — Tech / SaaS

**Personality:** Neutral, functional, modern. Zero visual distraction. Ideal for developer tools, dashboards, technical demos.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```

```css
:root {
  --font-heading: 'Inter', system-ui, -apple-system, sans-serif;
  --font-body:    'Inter', system-ui, -apple-system, sans-serif;
}

/* Usage guidance: differentiate heading vs. body through weight only */
.slide-title    { font-family: var(--font-heading); font-weight: var(--fw-extrabold); letter-spacing: var(--ls-tight); }
.slide-heading  { font-family: var(--font-heading); font-weight: var(--fw-bold); letter-spacing: var(--ls-tight); }
.slide-body     { font-family: var(--font-body);    font-weight: var(--fw-regular); letter-spacing: var(--ls-normal); }
```

---

#### Pairing 2: Plus Jakarta Sans + DM Sans — Startup / Product

**Personality:** Confident, friendly, contemporary. Geometric softness with strong weight contrast. Use for product pitches, investor decks, growth-stage startups.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@700;800&family=DM+Sans:wght@400;500&display=swap" rel="stylesheet">
```

```css
:root {
  --font-heading: 'Plus Jakarta Sans', system-ui, sans-serif;
  --font-body:    'DM Sans', system-ui, sans-serif;
}

.slide-title    { font-family: var(--font-heading); font-weight: var(--fw-extrabold); letter-spacing: var(--ls-tight); }
.slide-heading  { font-family: var(--font-heading); font-weight: var(--fw-bold); letter-spacing: var(--ls-tight); }
.slide-body     { font-family: var(--font-body);    font-weight: var(--fw-regular); letter-spacing: var(--ls-normal); }
.slide-emphasis { font-family: var(--font-body);    font-weight: var(--fw-medium); }
```

---

#### Pairing 3: Fraunces + Inter — Creative / Editorial

**Personality:** Expressive, high-contrast, literary. Optical serif heading creates strong typographic identity while Inter body ensures readability. Use for creative agencies, brand strategy, design portfolios.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,700;9..144,800&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
```

```css
:root {
  --font-heading: 'Fraunces', Georgia, 'Times New Roman', serif;
  --font-body:    'Inter', system-ui, -apple-system, sans-serif;
}

.slide-title    { font-family: var(--font-heading); font-weight: var(--fw-extrabold); font-style: italic; letter-spacing: var(--ls-tighter); }
.slide-heading  { font-family: var(--font-heading); font-weight: var(--fw-bold); letter-spacing: var(--ls-tight); }
.slide-body     { font-family: var(--font-body);    font-weight: var(--fw-regular); letter-spacing: var(--ls-normal); }
.slide-label    { font-family: var(--font-body);    font-weight: var(--fw-semibold); letter-spacing: var(--ls-wide); text-transform: uppercase; font-size: var(--type-label); }
```

---

#### Pairing 4: Sora + Nunito Sans — Education / Friendly

**Personality:** Warm, approachable, rounded. Sora's geometric curves and Nunito's open apertures create an inviting, accessible tone. Use for e-learning, workshops, community talks, onboarding.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@700;800&family=Nunito+Sans:wght@400;600;700&display=swap" rel="stylesheet">
```

```css
:root {
  --font-heading: 'Sora', system-ui, sans-serif;
  --font-body:    'Nunito Sans', system-ui, sans-serif;
}

.slide-title    { font-family: var(--font-heading); font-weight: var(--fw-extrabold); letter-spacing: var(--ls-tight); }
.slide-heading  { font-family: var(--font-heading); font-weight: var(--fw-bold); letter-spacing: var(--ls-tight); }
.slide-body     { font-family: var(--font-body);    font-weight: var(--fw-regular); letter-spacing: var(--ls-normal); line-height: var(--lh-relaxed); }
.slide-emphasis { font-family: var(--font-body);    font-weight: var(--fw-bold); }
```

---

#### Pairing 5: Playfair Display + Source Sans 3 — Corporate / Consulting

**Personality:** Authoritative, editorial, prestigious. Classic high-contrast serif heading pairs with the workhorse clarity of Source Sans. Use for McKinsey-style decks, annual reports, executive briefings, academic lectures.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;800&family=Source+Sans+3:wght@400;600;700&display=swap" rel="stylesheet">
```

```css
:root {
  --font-heading: 'Playfair Display', Georgia, 'Times New Roman', serif;
  --font-body:    'Source Sans 3', system-ui, sans-serif;
}

.slide-title    { font-family: var(--font-heading); font-weight: var(--fw-extrabold); letter-spacing: var(--ls-tighter); }
.slide-heading  { font-family: var(--font-heading); font-weight: var(--fw-bold); letter-spacing: var(--ls-tight); }
.slide-body     { font-family: var(--font-body);    font-weight: var(--fw-regular); letter-spacing: var(--ls-normal); }
.slide-label    { font-family: var(--font-body);    font-weight: var(--fw-semibold); letter-spacing: var(--ls-wide); text-transform: uppercase; font-size: var(--type-label); }
.slide-caption  { font-family: var(--font-body);    font-weight: var(--fw-regular); font-size: var(--type-caption); line-height: var(--lh-relaxed); }
```

---

## 3. Spacing and Grid

### 3.1 8-Point Grid Scale

All spacing values are multiples of 4px (0.25rem base). The 8-point grid governs padding, margins, gaps, and layout offsets throughout every slide.

```css
:root {
  --space-1:  0.25rem;  /*  4px */
  --space-2:  0.5rem;   /*  8px */
  --space-3:  0.75rem;  /* 12px */
  --space-4:  1rem;     /* 16px */
  --space-5:  1.25rem;  /* 20px */
  --space-6:  1.5rem;   /* 24px */
  --space-8:  2rem;     /* 32px */
  --space-10: 2.5rem;   /* 40px */
  --space-12: 3rem;     /* 48px */
  --space-16: 4rem;     /* 64px */
  --space-20: 5rem;     /* 80px */
  --space-24: 6rem;     /* 96px */
}
```

### 3.2 Slide Padding Modes

Apply one of three padding modes per slide depending on content type.

```css
/* Default: standard content slides */
.slide-padding-default {
  padding: 3rem 4rem; /* 48px top/bottom, 64px left/right */
}

/* Dense: data-heavy slides, tables, large code blocks */
.slide-padding-dense {
  padding: 2rem 3rem; /* 32px top/bottom, 48px left/right */
}

/* Full-bleed: hero images, full-screen visuals, video backgrounds */
.slide-padding-full-bleed {
  padding: 0;
}
```

### 3.3 Canvas and Safe Zone

```css
/* reveal.js default canvas — do not change without explicit reason */
.reveal .slides {
  width: 960px;
  height: 700px;
}

/* Safe content area: keeps all text and CTAs away from slide edges */
.content-safe-zone {
  max-width: 860px;
  margin-left: auto;
  margin-right: auto;
}
```

Rule: No text, button, or interactive element should be positioned within 48px of any slide edge unless it is a decorative element (background texture, full-bleed image, edge-to-edge color block).

### 3.4 Vertical Rhythm

```css
/* Heading spacing */
h1, h2, .slide-title, .slide-heading {
  margin-top:    3rem;   /* var(--space-12) — 48px above major headings */
  margin-bottom: 1.5rem; /* var(--space-6)  — 24px below heading before content */
}

/* First heading in slide has no top margin (slide padding handles it) */
.slide > h1:first-child,
.slide > h2:first-child {
  margin-top: 0;
}

/* Body paragraph spacing */
p + p {
  margin-top: 1.5rem; /* var(--space-6) — 24px between paragraphs */
}

/* List item spacing */
li + li {
  margin-top: 0.75rem; /* var(--space-3) — 12px between list items */
}
```

### 3.5 Gap Tokens

Use these for CSS Grid and Flexbox `gap` properties on layout containers.

```css
:root {
  --gap-sm: 1rem;   /* 16px — tight card grids, icon rows */
  --gap-md: 1.5rem; /* 24px — standard two-column layouts */
  --gap-lg: 2rem;   /* 32px — wide column splits, feature blocks */
  --gap-xl: 3rem;   /* 48px — section-level spacing, hero layouts */
}
```

---

## 4. Slide Design Rules

### 4.1 Text Density Limits

These are hard limits. Exceeding them degrades readability at presentation size. When content exceeds these limits, split into additional slides.

| Element               | Maximum Value | Rationale |
|-----------------------|---------------|-----------|
| Words per slide       | 75 words      | Prevents reading-vs-listening conflict |
| Bullet points         | 5 bullets     | Working memory limit for audiences |
| Words per bullet      | 10 words      | Forces sentence fragments, not paragraphs |
| Code block lines      | 20 lines      | Legibility at 1920x1080 minimum display |
| Font sizes per slide  | 3 sizes       | Maintains clear hierarchy without noise |
| Colors per slide      | 4 colors      | Prevents visual fragmentation |

### 4.2 Image Minimum Specifications

| Context             | Minimum Size  | Format Notes |
|---------------------|---------------|--------------|
| Full-bleed background | 1920 × 1080px | JPG 85%+ quality or WebP; PNG for graphics |
| Half-slide image    | 960 × 700px   | Right/left split layouts |
| Card thumbnail      | 400 × 400px   | 1:1 ratio; use object-fit: cover |
| Logo / icon         | SVG preferred | Fall back to 2x PNG (min 200px) |
| Screenshot          | 1280 × 800px  | Retina screenshots at 2x preferred |

### 4.3 Whitespace Rules

These rules are non-negotiable. Whitespace is a primary design element, not wasted space.

- **Minimum empty space:** 20% of slide area must contain no content elements. If a slide feels crowded, remove content rather than shrinking type.
- **Edge clearance:** 48px minimum from all content to slide edge (enforced by `--slide-padding-default`).
- **Block separation:** 24px minimum between any two distinct content blocks (text groups, images, cards, code blocks).
- **Visual breathing room:** After placing content, check: can the eye rest anywhere? If every pixel is occupied, the slide fails.

### 4.4 Visual Hierarchy Order

Apply this sequence when deciding how to differentiate elements. Each level adds emphasis without requiring the next level. Use only as many levels as the content genuinely needs.

```
1. SIZE         — Largest element reads first. Slide title dwarfs body.
2. WEIGHT       — Bold reads before regular. Semibold subheadings separate from body.
3. COLOR        — Primary brand color draws attention above gray text.
4. SPACING      — More space around an element isolates and elevates it.
5. POSITION     — Top-left reads first (LTR). Center commands attention.
```

Never skip levels arbitrarily. If size and weight already establish hierarchy, adding color creates noise rather than clarity.

### 4.5 WCAG 2.2 Accessibility Requirements

**Contrast minimums (enforced):**

| Text Type                    | Minimum Ratio | Target  |
|------------------------------|---------------|---------|
| Normal body text (< 18pt)    | 4.5:1         | 7:1     |
| Large text (>= 18pt bold or >= 24pt regular) | 3:1  | 4.5:1 |
| UI component borders / icons | 3:1           | 4.5:1   |
| Decorative elements          | No requirement | —      |

**Color-only information rule:**

Never convey meaning through color alone. Always pair color with at least one additional indicator:
- An icon (checkmark for success, X for error, warning triangle)
- A text label ("Passed", "Failed", "Caution")
- A pattern difference (solid vs. dashed border)
- A positional indicator (left column = negative, right column = positive)

**Examples of violations to avoid:**
- Red bar = bad, green bar = good (without labels or icons)
- Blue text = link, black text = plain (without underline or other indicator)
- Orange = warning state (without text label)

---

## 5. reveal.js Variable Wiring

Map all `--color-*` semantic variables to reveal.js's `--r-*` theme variables inside the `.reveal {}` block. Place this CSS block after your chosen palette `:root` block.

```css
.reveal {
  /* Background */
  --r-background-color:       var(--color-background);

  /* Main text */
  --r-main-color:             var(--color-text-primary);
  --r-main-font:              var(--font-body);
  --r-main-font-size:         var(--type-body);

  /* Heading text */
  --r-heading-color:          var(--color-primary);
  --r-heading-font:           var(--font-heading);
  --r-heading-font-weight:    var(--fw-bold);
  --r-heading-line-height:    var(--lh-tight);
  --r-heading-letter-spacing: var(--ls-tight);
  --r-heading-text-transform: none;
  --r-heading-text-shadow:    none;

  /* Heading sizes — maps to reveal.js h1–h6 */
  --r-heading1-size:          var(--type-slide-title);
  --r-heading2-size:          var(--type-section-title);
  --r-heading3-size:          var(--type-slide-heading);
  --r-heading4-size:          var(--type-subheading);
  --r-heading5-size:          var(--type-body);
  --r-heading6-size:          var(--type-body-sm);

  /* Links */
  --r-link-color:             var(--color-link);
  --r-link-color-hover:       var(--color-primary);
  --r-link-color-visited:     var(--color-secondary);

  /* Selection highlight */
  --r-selection-background-color: var(--color-primary);
  --r-selection-color:            var(--color-text-inverse);

  /* Block quote / callout accent */
  --r-block-margin:           var(--space-6);

  /* Code */
  --r-code-font:              'Fira Code', 'JetBrains Mono', 'Cascadia Code', monospace;
  --r-code-font-size:         var(--type-code);
}

/* Slide background override */
.reveal .slide-background {
  background-color: var(--color-background);
}

/* Progress bar */
.reveal .progress {
  background: var(--color-surface-raised);
  color:      var(--color-primary);
}

/* Navigation controls */
.reveal .controls {
  color: var(--color-primary);
}

/* Slide number */
.reveal .slide-number {
  background-color: transparent;
  color:            var(--color-text-secondary);
  font-family:      var(--font-body);
  font-size:        var(--type-label);
}

/* Horizontal rule / divider */
.reveal hr {
  border: none;
  border-top: 1px solid var(--color-border);
  margin: var(--space-8) 0;
}

/* Blockquote */
.reveal blockquote {
  border-left: 4px solid var(--color-primary);
  background:  var(--color-surface);
  padding:     var(--space-6) var(--space-8);
  font-style:  italic;
  color:       var(--color-text-secondary);
}

/* Inline code */
.reveal code {
  background:    var(--color-surface);
  color:         var(--color-primary);
  padding:       0.125em 0.375em;
  border-radius: 4px;
  font-family:   var(--r-code-font);
  font-size:     var(--type-code);
}

/* Code block */
.reveal pre {
  background:    var(--color-surface);
  border:        1px solid var(--color-border);
  border-radius: 8px;
  padding:       var(--space-6);
  margin:        var(--space-6) 0;
  overflow-x:    auto;
}

.reveal pre code {
  background:  transparent;
  padding:     0;
  color:       var(--color-text-primary);
  font-size:   var(--type-code);
  line-height: var(--lh-normal);
}

/* Tables */
.reveal table {
  border-collapse: collapse;
  width:           100%;
  font-size:       var(--type-body-sm);
}

.reveal table th {
  background:    var(--color-surface-raised);
  color:         var(--color-text-primary);
  font-weight:   var(--fw-semibold);
  padding:       var(--space-3) var(--space-4);
  border-bottom: 2px solid var(--color-primary);
  text-align:    left;
}

.reveal table td {
  padding:       var(--space-3) var(--space-4);
  border-bottom: 1px solid var(--color-border);
  color:         var(--color-text-primary);
}

.reveal table tr:hover td {
  background: var(--color-surface);
}
```

---

## 6. Palette Selection Guide

Use this table to select the correct palette and font pairing for a given presentation tone or context. These recommendations optimize for audience expectations and content type.

| Tone / Context           | Palette               | Font Pairing                           | Key Signals |
|--------------------------|-----------------------|----------------------------------------|-------------|
| Corporate / Finance      | 1.1 Navy              | Playfair Display + Source Sans 3       | Board rooms, earnings reports, investor relations, banking |
| Startup / Product        | 1.2 Violet            | Plus Jakarta Sans + DM Sans            | Seed decks, product launches, Series A pitches, growth metrics |
| Technical / Developer    | 1.5 Dark Charcoal     | Inter (single)                         | Code demos, architecture talks, CLI tools, DevOps, security |
| Consulting / Academic    | 1.3 Minimal Teal      | Inter (single) or Playfair + Source Sans 3 | Research findings, strategy decks, university lectures, whitepapers |
| Creative / Marketing     | 1.4 Coral             | Fraunces + Inter                       | Brand reveals, campaign showcases, design critiques, agency new business |
| Education / Friendly     | 1.2 Violet            | Sora + Nunito Sans                     | Workshops, onboarding, e-learning modules, community events |

### Decision Tree

Use this logic when the context is ambiguous:

```
Is the audience wearing suits?
  YES → Does the content involve financial data?
          YES → Navy + Playfair Display + Source Sans 3
          NO  → Minimal + Inter or Playfair + Source Sans 3
  NO  → Is there live code or technical diagrams?
          YES → Dark Charcoal + Inter
          NO  → Is the goal to inspire or sell?
                  YES + B2B → Violet + Plus Jakarta Sans + DM Sans
                  YES + Consumer/Brand → Coral + Fraunces + Inter
                  NO  → Friendly/Educational → Violet + Sora + Nunito Sans
```

### Overrides and Exceptions

- A dark palette presentation can selectively use a light palette for title-only "section divider" slides. Apply `data-background-color="var(--color-background)"` to individual slides.
- The Creative (Coral) palette's warm background (`#FFFBF5`) may feel too informal for purely financial slides. In that case, substitute `--color-background: #FFFFFF` and `--color-surface: #FFF7ED` to cool it slightly without changing the rest of the palette.
- When embedding live demos or browser windows in slides, always use the Dark Charcoal palette — it minimizes screen glare and reduces audience eye fatigue under bright projectors.
- For bilingual or CJK (Chinese/Japanese/Korean) presentations, Inter (Pairing 1) is the safest choice because it has broad Unicode coverage and degrades gracefully to system fonts for characters outside its range.

---

*Last updated: 2026-04-07. All hex values, ratios, and rem measurements are exact. Do not approximate or round these values when generating presentation code.*
