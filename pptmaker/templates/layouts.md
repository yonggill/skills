# Slide Layouts Reference

All CSS properties must use `var()` references to design system tokens. Never use hardcoded colors, sizes, or spacing values except for specific structural values like percentages, pixel dimensions on fixed-size decorative elements, or neutral dark code editor backgrounds. Token categories: `--color-*`, `--type-*`, `--space-*`, `--fw-*`, `--lh-*`, `--ls-*`, `--gap-*`.

---

## 1. Title Slide (`.layout-title`)

Full-bleed primary-color background. Left-aligned with large hero heading, eyebrow label, subtitle, and author/date meta row.

### HTML

```html
<section class="layout-title" data-background-color="var(--color-primary)">
  <p class="title-eyebrow">Product Launch · Q2 2026</p>
  <h1 class="title-main">Transforming How Teams Build Together</h1>
  <p class="title-subtitle">
    A unified platform for design, development, and delivery —
    shipping faster without sacrificing quality.
  </p>
  <div class="title-meta">
    <span class="title-author">Jane Kim</span>
    <span class="title-divider">|</span>
    <span class="title-date">April 7, 2026</span>
  </div>
</section>
```

### CSS

```css
/* ── Title Slide ──────────────────────────────────────────────────── */
.layout-title {
  justify-content: center;
  align-items: flex-start;
  padding: 3rem 4rem;
  gap: var(--space-5);
  text-align: left;
}

.title-eyebrow {
  font-size: var(--type-label);
  font-weight: var(--fw-semibold);
  letter-spacing: var(--ls-wider);
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.65);
  margin: 0;
  overflow-wrap: break-word;
}

.title-main {
  font-size: var(--type-slide-title);
  font-weight: var(--fw-extrabold);
  line-height: var(--lh-tight);
  letter-spacing: var(--ls-tighter);
  color: white;
  max-width: 80%;
  margin: 0;
  overflow-wrap: break-word;
}

.title-subtitle {
  font-size: var(--type-body);
  line-height: var(--lh-relaxed);
  color: rgba(255, 255, 255, 0.80);
  max-width: 60%;
  margin: 0;
  overflow-wrap: break-word;
}

.title-meta {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: var(--space-3);
  margin-top: var(--space-2);
}

.title-author,
.title-divider,
.title-date {
  font-size: var(--type-body-sm);
  color: rgba(255, 255, 255, 0.60);
}

.title-divider {
  opacity: 0.4;
}
```

---

## 2. Section Divider (`.layout-section-divider`)

Full-bleed primary-color background with a large ghost number, section title, and short description. Used between major presentation sections.

### HTML

```html
<section class="layout-section-divider" data-background-color="var(--color-primary)">
  <div class="section-number" aria-hidden="true">02</div>
  <h2 class="section-title">Market Opportunity</h2>
  <p class="section-description">
    Exploring the $42B addressable market and the structural shifts that open the door for a new category leader.
  </p>
</section>
```

### CSS

```css
/* ── Section Divider ──────────────────────────────────────────────── */
.layout-section-divider {
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 3rem 4rem;
  gap: var(--space-4);
  position: relative;
}

.section-number {
  font-size: 12rem;
  font-weight: var(--fw-extrabold);
  line-height: 1;
  color: rgba(255, 255, 255, 0.08);
  letter-spacing: var(--ls-tighter);
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
  user-select: none;
  z-index: 0;
}

.section-title {
  font-size: var(--type-section-title);
  font-weight: var(--fw-bold);
  line-height: var(--lh-tight);
  color: white;
  margin: 0;
  position: relative;
  z-index: 1;
  overflow-wrap: break-word;
}

.section-description {
  font-size: var(--type-body);
  line-height: var(--lh-relaxed);
  color: rgba(255, 255, 255, 0.70);
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
  word-break: keep-all;
  position: relative;
  z-index: 1;
  overflow-wrap: break-word;
}
```

---

## 3. Text + Image (`.layout-text-image`)

Two-column grid: text on the left, image on the right. Includes a reversed variant (`.layout-image-text`) where image appears on the left.

### HTML

```html
<!-- Text left, image right -->
<section class="layout-text-image">
  <div class="text-col">
    <p class="slide-eyebrow">Platform Overview</p>
    <h2 class="slide-heading">One canvas. Every workflow.</h2>
    <p class="slide-body">
      Bring design files, component libraries, and live code into a single
      shared environment. No more switching between six tools — everything
      your team needs lives in one place.
    </p>
    <ul class="slide-bullets">
      <li>Real-time multiplayer editing</li>
      <li>Version-controlled component system</li>
      <li>One-click handoff to engineering</li>
    </ul>
  </div>
  <div class="image-col">
    <img
      class="slide-img"
      src="path/to/product-screenshot.jpg"
      alt="Product interface showing the unified canvas with design and code panels side by side"
    />
  </div>
</section>

<!-- Image left, text right (reversed variant) -->
<section class="layout-image-text">
  <div class="image-col">
    <img
      class="slide-img"
      src="path/to/product-screenshot.jpg"
      alt="Descriptive alt text"
    />
  </div>
  <div class="text-col">
    <p class="slide-eyebrow">Integrations</p>
    <h2 class="slide-heading">Plugs into tools you already use.</h2>
    <p class="slide-body">
      Native integrations with GitHub, Figma, Jira, and Slack mean your
      existing workflows stay intact — we just make them faster.
    </p>
  </div>
</section>
```

### CSS

```css
/* ── Text + Image ─────────────────────────────────────────────────── */
.layout-text-image,
.layout-image-text {
  display: grid !important;
  flex-direction: row;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
  padding: 2rem 3rem;
  align-items: center;
}

/* Reversed layout — RTL trick keeps DOM order semantic */
.layout-image-text {
  direction: rtl;
}

.layout-image-text .text-col,
.layout-image-text .image-col {
  direction: ltr;
}

.text-col {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: var(--space-4);
  min-width: 0;
  overflow: hidden;
  overflow-wrap: break-word;
}

.slide-eyebrow {
  font-size: var(--type-label);
  font-weight: var(--fw-semibold);
  letter-spacing: var(--ls-wider);
  text-transform: uppercase;
  color: var(--color-primary);
  margin: 0;
}

.slide-heading {
  font-size: var(--type-slide-heading);
  font-weight: var(--fw-bold);
  line-height: var(--lh-tight);
  letter-spacing: var(--ls-tight);
  color: var(--color-text-primary);
  margin: 0;
  overflow-wrap: break-word;
}

.slide-body {
  font-size: var(--type-body);
  line-height: var(--lh-relaxed);
  color: var(--color-text-secondary);
  margin: 0;
  overflow-wrap: break-word;
}

.slide-bullets {
  font-size: var(--type-body-sm);
  line-height: var(--lh-relaxed);
  color: var(--color-text-secondary);
  padding-left: var(--space-5);
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
}

.image-col {
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  border-radius: 0.75rem;
  max-height: 520px;
  min-width: 0;
}

.slide-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 0.75rem;
  display: block;
}
```

---

## 4. Two-Column Comparison (`.layout-two-col`)

Side-by-side comparison of two options, approaches, or entities. Each column has a labeled header card and a body content card.

### HTML

```html
<section class="layout-two-col">
  <header class="slide-header">
    <h2 class="slide-heading">Legacy Approach vs. Modern Platform</h2>
  </header>

  <div class="col-header">
    <div class="col-label col-label--neutral">Before</div>
    <div class="col-label col-label--accent">After</div>
  </div>

  <div class="col-body">
    <!-- Left column card -->
    <div class="col-card">
      <ul class="col-list">
        <li>Siloed design and engineering tools</li>
        <li>Manual handoff via exported assets</li>
        <li>No shared component source of truth</li>
        <li>Weeks of QA chasing pixel drift</li>
        <li>Onboarding takes 3–4 weeks</li>
      </ul>
    </div>

    <!-- Right column card (accented) -->
    <div class="col-card col-card--accent">
      <ul class="col-list col-list--check">
        <li>Unified canvas for design and code</li>
        <li>One-click automated handoff</li>
        <li>Single versioned component library</li>
        <li>Built-in visual regression testing</li>
        <li>Onboarding in under 2 days</li>
      </ul>
    </div>
  </div>
</section>
```

### CSS

```css
/* ── Two-Column Comparison ────────────────────────────────────────── */
.layout-two-col {
  justify-content: flex-start;
  gap: 0.75rem;
}

.col-header {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  width: 100%;
  min-width: 0;
}

.col-body {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  width: 100%;
  min-width: 0;
}

.col-label {
  font-size: var(--type-subheading);
  font-weight: var(--fw-bold);
  text-align: center;
  padding: 0.75rem 1rem;
  border-radius: 0.5rem 0.5rem 0 0;
  border-bottom: 3px solid var(--color-border);
  color: var(--color-text-secondary);
  background: var(--color-surface);
}

.col-label--accent {
  border-bottom-color: var(--color-primary);
  color: var(--color-primary);
  background: color-mix(in srgb, var(--color-primary) 6%, var(--color-background));
}

.col-card {
  background: var(--color-surface);
  border-radius: 0 0 0.75rem 0.75rem;
  padding: 1.5rem;
  border: 2px solid var(--color-border);
  border-top: none;
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
  min-width: 0;
  overflow: hidden;
  overflow-wrap: break-word;
}

.col-card--accent {
  border-color: var(--color-primary);
  background: color-mix(in srgb, var(--color-primary) 5%, var(--color-background));
}

.col-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}

.col-list li {
  font-size: var(--type-body-sm);
  line-height: var(--lh-snug);
  color: var(--color-text-secondary);
  padding-left: var(--space-4);
  position: relative;
}

.col-list li::before {
  content: "–";
  position: absolute;
  left: 0;
  color: var(--color-border);
  font-weight: var(--fw-bold);
}

.col-list--check li::before {
  content: "✓";
  color: var(--color-success);
}
```

---

## 5. Three-Column Features (`.layout-three-col`)

Three equal-width feature cards in a single row, each with an icon, title, and description. Pairs with the `.feature-card` component from `components.md`.

### HTML

```html
<section class="layout-three-col">
  <header class="slide-header">
    <h2 class="slide-heading">Why teams choose us</h2>
    <p class="slide-subheading">Three core pillars that set the platform apart.</p>
  </header>

  <div class="three-col-grid">
    <div class="feature-card">
      <div class="feature-icon-wrap">
        <svg class="feature-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
          <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/>
        </svg>
      </div>
      <h3 class="feature-title">10× Faster Handoff</h3>
      <p class="feature-desc">Automated token extraction and code generation eliminates manual spec writing for good.</p>
    </div>

    <div class="feature-card">
      <div class="feature-icon-wrap">
        <svg class="feature-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
          <circle cx="12" cy="12" r="3"/>
          <path d="M19.07 4.93a10 10 0 0 1 0 14.14"/>
          <path d="M4.93 4.93a10 10 0 0 0 0 14.14"/>
        </svg>
      </div>
      <h3 class="feature-title">Always in Sync</h3>
      <p class="feature-desc">Design and code stay connected at the token level — update once, propagate everywhere.</p>
    </div>

    <div class="feature-card">
      <div class="feature-icon-wrap">
        <svg class="feature-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
          <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/>
        </svg>
      </div>
      <h3 class="feature-title">Enterprise-Grade Security</h3>
      <p class="feature-desc">SOC 2 Type II certified with SSO, RBAC, and audit logs included in every plan.</p>
    </div>
  </div>
</section>
```

### CSS

```css
/* ── Three-Column Features ────────────────────────────────────────── */
.layout-three-col {
  justify-content: flex-start;
  gap: 1rem;
}

.slide-header {
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
}

.slide-subheading {
  font-size: var(--type-body);
  color: var(--color-text-secondary);
  margin: 0;
  overflow-wrap: break-word;
}

.three-col-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  width: 100%;
  min-width: 0;
  overflow: hidden;
}

.feature-card {
  min-width: 0;
  overflow: hidden;
  overflow-wrap: break-word;
}
```

---

## 6. Full-Image with Overlay (`.layout-full-image`)

Full-bleed background image set via `data-background-image` on the `<section>`. A gradient scrim ensures text legibility. Content is anchored to the bottom-left.

### HTML

```html
<section
  class="layout-full-image"
  data-background-image="path/to/hero-photo.jpg"
  data-background-size="cover"
  data-background-position="center"
>
  <div class="overlay-scrim" aria-hidden="true"></div>
  <div class="overlay-content">
    <p class="overlay-eyebrow">Case Study · Enterprise</p>
    <h2 class="overlay-heading">
      How Acme Corp shipped a design system in 6 weeks
    </h2>
    <p class="overlay-body">
      A cross-functional team of 4 designers and 6 engineers — zero external consultants.
    </p>
  </div>
</section>
```

### CSS

```css
/* ── Full-Image with Overlay ──────────────────────────────────────── */
.layout-full-image {
  position: relative;
  align-items: flex-start;
  justify-content: flex-end;
  padding: 0 !important;
}

.overlay-scrim {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to top,
    rgba(0, 0, 0, 0.80) 0%,
    rgba(0, 0, 0, 0.40) 50%,
    rgba(0, 0, 0, 0.05) 100%
  );
  z-index: 1;
}

.overlay-content {
  position: relative;
  z-index: 2;
  padding: 3rem 4rem;
  text-align: left;
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
}

.overlay-eyebrow {
  font-size: var(--type-label);
  font-weight: var(--fw-semibold);
  letter-spacing: var(--ls-wider);
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.75);
  margin: 0;
}

.overlay-heading {
  font-size: var(--type-section-title);
  font-weight: var(--fw-bold);
  line-height: var(--lh-tight);
  color: white;
  max-width: 700px;
  margin: 0;
}

.overlay-body {
  font-size: var(--type-body);
  line-height: var(--lh-relaxed);
  color: rgba(255, 255, 255, 0.80);
  max-width: 600px;
  margin: 0;
}
```

---

## 7. Quote / Testimonial (`.layout-quote`)

Centered full-slide quote with large decorative quotation mark, attributed to a person with avatar, name, and role.

### HTML

```html
<section class="layout-quote">
  <div class="quote-block">
    <div class="quote-mark" aria-hidden="true">"</div>
    <blockquote class="quote-text">
      The platform cut our design-to-dev cycle from three weeks to four days.
      I genuinely can't imagine going back to the way we worked before.
    </blockquote>
    <div class="quote-attribution">
      <img
        class="quote-avatar"
        src="path/to/avatar.jpg"
        alt="Portrait of Sarah Chen"
        width="56"
        height="56"
      />
      <div class="quote-identity">
        <span class="quote-name">Sarah Chen</span>
        <span class="quote-role">VP of Product, Horizon Health</span>
      </div>
    </div>
  </div>
</section>
```

### CSS

```css
/* ── Quote / Testimonial ──────────────────────────────────────────── */
.layout-quote {
  justify-content: center;
  align-items: center;
}

.quote-block {
  max-width: 700px;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-5);
  overflow-wrap: break-word;
}

.quote-mark {
  font-size: 8rem;
  line-height: 0.6;
  font-family: Georgia, 'Times New Roman', serif;
  color: var(--color-primary);
  opacity: 0.4;
  display: block;
  align-self: center;
  margin-bottom: calc(-1 * var(--space-3));
}

.quote-text {
  font-size: var(--type-slide-heading);
  font-weight: var(--fw-medium);
  line-height: var(--lh-snug);
  font-style: italic;
  color: var(--color-text-primary);
  margin: 0;
  quotes: none;
}

.quote-attribution {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-4);
}

.quote-avatar {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid var(--color-border);
  flex-shrink: 0;
}

.quote-identity {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: var(--space-1);
  text-align: left;
}

.quote-name {
  font-size: var(--type-body);
  font-weight: var(--fw-semibold);
  color: var(--color-text-primary);
}

.quote-role {
  font-size: var(--type-caption);
  color: var(--color-text-secondary);
}
```

---

## 8. KPI Dashboard (`.kpi-grid-*`)

Four grid variants for arranging `.kpi-card` components (defined in `components.md`). Choose the variant that best matches the number of KPIs to display.

### HTML

```html
<!-- 2×2 grid: 4 equal cards -->
<section class="layout-kpi">
  <header class="slide-header">
    <h2 class="slide-heading">Q1 2026 Performance</h2>
  </header>
  <div class="kpi-grid-2x2">
    <div class="kpi-card">
      <div class="kpi-icon">💰</div>
      <div class="kpi-number">$4.2M</div>
      <div class="kpi-label">Annual Recurring Revenue</div>
      <div class="kpi-delta kpi-delta--up">▲ 18% vs last quarter</div>
    </div>
    <div class="kpi-card">
      <div class="kpi-icon">👥</div>
      <div class="kpi-number">1,840</div>
      <div class="kpi-label">Active Customers</div>
      <div class="kpi-delta kpi-delta--up">▲ 12% vs last quarter</div>
    </div>
    <div class="kpi-card">
      <div class="kpi-icon">📉</div>
      <div class="kpi-number">1.4%</div>
      <div class="kpi-label">Monthly Churn Rate</div>
      <div class="kpi-delta kpi-delta--down">▼ 0.3pp improvement</div>
    </div>
    <div class="kpi-card">
      <div class="kpi-icon">⭐</div>
      <div class="kpi-number">4.8</div>
      <div class="kpi-label">Average NPS Score</div>
      <div class="kpi-delta kpi-delta--up">▲ 0.4 vs last quarter</div>
    </div>
  </div>
</section>

<!-- 1×3 grid: 3 equal cards in a single row -->
<section class="layout-kpi">
  <header class="slide-header">
    <h2 class="slide-heading">Engineering Health</h2>
  </header>
  <div class="kpi-grid-1x3">
    <div class="kpi-card"><!-- ... --></div>
    <div class="kpi-card"><!-- ... --></div>
    <div class="kpi-card"><!-- ... --></div>
  </div>
</section>

<!-- 1×4 grid: 4 compact cards in a single row -->
<section class="layout-kpi">
  <div class="kpi-grid-1x4">
    <div class="kpi-card"><!-- ... --></div>
    <div class="kpi-card"><!-- ... --></div>
    <div class="kpi-card"><!-- ... --></div>
    <div class="kpi-card"><!-- ... --></div>
  </div>
</section>

<!-- Featured grid: 1 hero card + 2 supporting cards -->
<section class="layout-kpi">
  <div class="kpi-grid-featured">
    <!-- First child automatically spans 2 rows -->
    <div class="kpi-card kpi-card--hero">
      <div class="kpi-icon">🚀</div>
      <div class="kpi-number">$4.2M</div>
      <div class="kpi-label">Annual Recurring Revenue</div>
      <div class="kpi-delta kpi-delta--up">▲ 18% vs last quarter</div>
    </div>
    <div class="kpi-card"><!-- supporting card 1 --></div>
    <div class="kpi-card"><!-- supporting card 2 --></div>
  </div>
</section>
```

### CSS

```css
/* ── KPI Dashboard Layout ─────────────────────────────────────────── */
.layout-kpi {
  justify-content: flex-start;
  gap: 1rem;
}

/* 2×2 — two columns, two rows */
.kpi-grid-2x2 {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
  gap: 1rem;
  width: 100%;
}

/* 1×3 — three equal columns, single row */
.kpi-grid-1x3 {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  width: 100%;
}

/* 1×4 — four compact columns, single row */
.kpi-grid-1x4 {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
  width: 100%;
}

/* Featured — one hero card spanning 2 rows + 2 supporting cards */
.kpi-grid-featured {
  display: grid;
  grid-template-columns: 2fr 1fr;
  grid-template-rows: repeat(2, 1fr);
  gap: 1rem;
  width: 100%;
}

.kpi-grid-featured > :first-child {
  grid-row: 1 / 3;
}

/* All KPI cards prevent overflow */
.kpi-card {
  min-width: 0;
  overflow: hidden;
  overflow-wrap: break-word;
}

/* Hero card enlarges the number */
.kpi-card--hero .kpi-number {
  font-size: calc(var(--type-kpi-number) * 1.4);
}
```

---

## 9. Timeline (`.timeline-h` / `.timeline-v`)

Two orientations: horizontal for sequential milestones across the top of a slide, vertical for step-by-step lists.

### HTML

```html
<!-- Horizontal timeline -->
<section class="layout-timeline">
  <header class="slide-header">
    <h2 class="slide-heading">Product Roadmap 2026</h2>
  </header>
  <div class="timeline-h">
    <div class="timeline-item">
      <div class="timeline-dot" aria-hidden="true"></div>
      <span class="timeline-date">Q1 2026</span>
      <span class="timeline-event">Design system v2 launch</span>
    </div>
    <div class="timeline-item">
      <div class="timeline-dot" aria-hidden="true"></div>
      <span class="timeline-date">Q2 2026</span>
      <span class="timeline-event">Mobile SDK beta</span>
    </div>
    <div class="timeline-item">
      <div class="timeline-dot" aria-hidden="true"></div>
      <span class="timeline-date">Q3 2026</span>
      <span class="timeline-event">Enterprise SSO + SCIM</span>
    </div>
    <div class="timeline-item">
      <div class="timeline-dot" aria-hidden="true"></div>
      <span class="timeline-date">Q4 2026</span>
      <span class="timeline-event">AI co-pilot GA release</span>
    </div>
  </div>
</section>

<!-- Vertical timeline -->
<section class="layout-timeline">
  <header class="slide-header">
    <h2 class="slide-heading">How we got here</h2>
  </header>
  <div class="timeline-v">
    <div class="timeline-item">
      <div class="timeline-dot" aria-hidden="true"></div>
      <div class="timeline-body">
        <span class="timeline-date">March 2022</span>
        <span class="timeline-event">Company founded with seed funding</span>
      </div>
    </div>
    <div class="timeline-item">
      <div class="timeline-dot" aria-hidden="true"></div>
      <div class="timeline-body">
        <span class="timeline-date">September 2023</span>
        <span class="timeline-event">Series A — $12M raised</span>
      </div>
    </div>
    <div class="timeline-item">
      <div class="timeline-dot" aria-hidden="true"></div>
      <div class="timeline-body">
        <span class="timeline-date">January 2025</span>
        <span class="timeline-event">1,000 paying customers milestone</span>
      </div>
    </div>
    <div class="timeline-item">
      <div class="timeline-dot" aria-hidden="true"></div>
      <div class="timeline-body">
        <span class="timeline-date">April 2026</span>
        <span class="timeline-event">Series B — $40M raised</span>
      </div>
    </div>
  </div>
</section>
```

### CSS

```css
/* ── Timeline Layout ──────────────────────────────────────────────── */
.layout-timeline {
  justify-content: flex-start;
  gap: var(--space-6);
}

/* Horizontal */
.timeline-h {
  display: flex;
  flex-direction: row;
  position: relative;
  padding-top: 3rem;
  width: 100%;
  min-width: 0;
  align-items: flex-start;
}

/* Connecting line across the top */
.timeline-h::before {
  content: "";
  position: absolute;
  top: 1.25rem;
  left: 0;
  right: 0;
  height: 3px;
  background: var(--color-border);
}

.timeline-h .timeline-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: var(--space-2);
  padding-top: 2rem;
  position: relative;
  min-width: 0;
  overflow-wrap: break-word;
}

.timeline-h .timeline-dot {
  position: absolute;
  top: -0.75rem;
  left: 50%;
  transform: translateX(-50%);
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: var(--color-primary);
  border: 4px solid var(--color-background);
  box-shadow: 0 0 0 3px var(--color-primary);
}

/* Vertical */
.timeline-v {
  display: flex;
  flex-direction: column;
  position: relative;
  padding-left: 3rem;
  gap: var(--space-5);
  width: 100%;
  min-width: 0;
}

/* Connecting line down the left */
.timeline-v::before {
  content: "";
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0.875rem;
  width: 3px;
  background: var(--color-border);
}

.timeline-v .timeline-item {
  display: flex;
  flex-direction: row;
  gap: var(--space-6);
  align-items: flex-start;
  position: relative;
  min-width: 0;
  overflow-wrap: break-word;
}

.timeline-v .timeline-dot {
  position: absolute;
  left: calc(-3rem + 0.875rem - 10px);
  top: 0.2rem;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: var(--color-primary);
  border: 4px solid var(--color-background);
  box-shadow: 0 0 0 3px var(--color-primary);
  flex-shrink: 0;
}

/* Shared item content */
.timeline-date {
  font-size: var(--type-label);
  font-weight: var(--fw-semibold);
  text-transform: uppercase;
  letter-spacing: var(--ls-wide);
  color: var(--color-text-secondary);
}

.timeline-event {
  font-size: var(--type-body-sm);
  font-weight: var(--fw-medium);
  text-align: center;
  color: var(--color-text-primary);
}

.timeline-body {
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
}

.timeline-v .timeline-event {
  text-align: left;
}
```

---

## 10. Process / Flow (`.process-flow`)

Horizontal sequence of numbered steps connected by arrows. For up to 5 steps.

### HTML

```html
<section class="layout-process">
  <header class="slide-header">
    <h2 class="slide-heading">How it works</h2>
    <p class="slide-subheading">From first login to shipped code in four steps.</p>
  </header>

  <div class="process-flow">
    <div class="process-step">
      <div class="process-icon" aria-label="Step 1">1</div>
      <span class="process-label">Connect</span>
      <p class="process-desc">Link your Figma workspace and GitHub repositories</p>
    </div>

    <div class="process-arrow" aria-hidden="true">→</div>

    <div class="process-step">
      <div class="process-icon" aria-label="Step 2">2</div>
      <span class="process-label">Configure</span>
      <p class="process-desc">Map design tokens to your codebase conventions</p>
    </div>

    <div class="process-arrow" aria-hidden="true">→</div>

    <div class="process-step">
      <div class="process-icon" aria-label="Step 3">3</div>
      <span class="process-label">Generate</span>
      <p class="process-desc">Auto-produce components, specs, and changelogs</p>
    </div>

    <div class="process-arrow" aria-hidden="true">→</div>

    <div class="process-step">
      <div class="process-icon" aria-label="Step 4">4</div>
      <span class="process-label">Ship</span>
      <p class="process-desc">Open a PR with pixel-perfect components, ready to merge</p>
    </div>
  </div>
</section>
```

### CSS

```css
/* ── Process / Flow ───────────────────────────────────────────────── */
.layout-process {
  justify-content: flex-start;
  gap: 1rem;
}

.process-flow {
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  justify-content: center;
  width: 100%;
  min-width: 0;
  overflow: hidden;
}

.process-step {
  flex: 1 1 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: var(--space-3);
  min-width: 0;
  overflow: hidden;
}

.process-icon {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background: var(--color-primary);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: var(--type-subheading);
  font-weight: var(--fw-bold);
  line-height: 1;
  flex-shrink: 0;
}

.process-label {
  font-size: var(--type-body-sm);
  font-weight: var(--fw-semibold);
  color: var(--color-text-primary);
  overflow-wrap: break-word;
}

.process-desc {
  font-size: 0.75rem;
  line-height: var(--lh-relaxed);
  color: var(--color-text-secondary);
  max-width: none;
  margin: 0;
  word-break: keep-all;
  overflow-wrap: break-word;
}

.process-arrow {
  flex: 0 0 auto;
  font-size: 1rem;
  color: var(--color-border);
  align-self: center;
  margin-top: calc(-1 * var(--space-6));
  line-height: 1;
}
```

---

## 11. Code Showcase (`.layout-code`)

Split view with a code editor pane on the left and a rendered result or annotation pane on the right. The code background uses a neutral dark editor color `#1E1E2E` that is intentionally not a design token — it is a fixed code editor aesthetic value.

### HTML

```html
<section class="layout-code">
  <header class="slide-header">
    <h2 class="slide-heading">Design tokens in code</h2>
    <p class="slide-subheading">Tokens flow directly from Figma into your component library.</p>
  </header>

  <div class="code-showcase-grid">
    <!-- Code pane -->
    <div class="code-pane">
      <div class="code-pane-header">
        <span class="code-filename">tokens.css</span>
      </div>
      <pre><code class="language-css">:root {
  --color-primary:   #6366F1;
  --color-surface:   #F8F8FF;
  --type-body:       1rem;
  --fw-semibold:     600;
  --space-4:         1rem;
  --gap-md:          1.5rem;
}

.button-primary {
  background: var(--color-primary);
  font-weight: var(--fw-semibold);
  padding: var(--space-4) var(--gap-md);
}</code></pre>
    </div>

    <!-- Result pane -->
    <div class="code-result-pane">
      <div class="code-pane-header">
        <span class="code-filename">Preview</span>
      </div>
      <div class="code-result-body">
        <!-- Place rendered component preview or annotation list here -->
        <ul class="code-annotation-list">
          <li><span class="code-token-ref">--color-primary</span> drives all interactive elements</li>
          <li><span class="code-token-ref">--fw-semibold</span> enforces consistent button weight</li>
          <li><span class="code-token-ref">--space-4</span> standardises vertical rhythm</li>
        </ul>
      </div>
    </div>
  </div>
</section>
```

### CSS

```css
/* ── Code Showcase ────────────────────────────────────────────────── */
.layout-code {
  justify-content: flex-start;
  gap: 1rem;
}

.code-showcase-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  width: 100%;
  min-width: 0;
  overflow: hidden;
}

.code-pane,
.code-result-pane {
  display: flex;
  flex-direction: column;
  border-radius: 0.75rem;
  overflow: hidden;
  border: 1px solid var(--color-border);
  min-width: 0;
}

.code-pane-header {
  display: flex;
  align-items: center;
  background: var(--color-surface-raised);
  padding: 0.5rem 1rem;
  border-bottom: 1px solid var(--color-border);
  flex-shrink: 0;
}

.code-filename {
  font-size: var(--type-caption);
  font-family: 'JetBrains Mono', 'Fira Code', monospace;
  color: var(--color-text-secondary);
}

.code-pane pre {
  margin: 0;
  /* Intentional fixed value: neutral dark code editor background */
  background: #1E1E2E;
  font-size: var(--type-code);
  line-height: 1.6;
  padding: 1.25rem;
  overflow: auto;
  flex: 1;
}

.code-result-pane .code-result-body {
  flex: 1;
  padding: 1.25rem;
  background: var(--color-surface);
  overflow: auto;
}

.code-annotation-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
}

.code-annotation-list li {
  font-size: var(--type-body-sm);
  line-height: var(--lh-relaxed);
  color: var(--color-text-secondary);
}

.code-token-ref {
  font-family: 'JetBrains Mono', 'Fira Code', monospace;
  font-size: var(--type-caption);
  background: color-mix(in srgb, var(--color-primary) 10%, var(--color-background));
  color: var(--color-primary);
  padding: 0.15em 0.4em;
  border-radius: 0.25rem;
  white-space: nowrap;
}
```

---

## 12. Team Grid (`.team-grid`)

Responsive grid of team member cards. Auto-fills available space with minimum 160px card width.

### HTML

```html
<section class="layout-team">
  <header class="slide-header">
    <h2 class="slide-heading">Meet the leadership team</h2>
  </header>

  <div class="team-grid">
    <div class="team-card">
      <img class="team-avatar" src="path/to/jane.jpg" alt="Portrait of Jane Kim" width="100" height="100" />
      <span class="team-name">Jane Kim</span>
      <span class="team-role">CEO &amp; Co-Founder</span>
    </div>
    <div class="team-card">
      <img class="team-avatar" src="path/to/marcus.jpg" alt="Portrait of Marcus Reed" width="100" height="100" />
      <span class="team-name">Marcus Reed</span>
      <span class="team-role">CTO &amp; Co-Founder</span>
    </div>
    <div class="team-card">
      <img class="team-avatar" src="path/to/priya.jpg" alt="Portrait of Priya Nair" width="100" height="100" />
      <span class="team-name">Priya Nair</span>
      <span class="team-role">VP of Product</span>
    </div>
    <div class="team-card">
      <img class="team-avatar" src="path/to/daniel.jpg" alt="Portrait of Daniel Park" width="100" height="100" />
      <span class="team-name">Daniel Park</span>
      <span class="team-role">VP of Engineering</span>
    </div>
    <div class="team-card">
      <img class="team-avatar" src="path/to/sofia.jpg" alt="Portrait of Sofia Morales" width="100" height="100" />
      <span class="team-name">Sofia Morales</span>
      <span class="team-role">Head of Design</span>
    </div>
    <div class="team-card">
      <img class="team-avatar" src="path/to/leo.jpg" alt="Portrait of Leo Zhang" width="100" height="100" />
      <span class="team-name">Leo Zhang</span>
      <span class="team-role">Head of Revenue</span>
    </div>
  </div>
</section>
```

### CSS

```css
/* ── Team Grid ────────────────────────────────────────────────────── */
.layout-team {
  justify-content: flex-start;
  gap: var(--space-6);
}

.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  gap: 1rem;
  width: 100%;
  min-width: 0;
  align-content: start;
}

.team-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: var(--space-3);
  padding: 1.5rem 1rem;
  border-radius: 0.75rem;
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  min-width: 0;
  overflow: hidden;
  overflow-wrap: break-word;
}

.team-avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid var(--color-surface-raised);
  display: block;
}

.team-name {
  font-size: var(--type-body-sm);
  font-weight: var(--fw-semibold);
  color: var(--color-text-primary);
  line-height: var(--lh-snug);
}

.team-role {
  font-size: var(--type-caption);
  color: var(--color-text-secondary);
  line-height: var(--lh-snug);
}
```

---

## 13. Pricing Table (`.pricing-grid`)

Three-column pricing card grid with a featured/highlighted tier. The featured card is visually elevated with a border, tint, scale, and shadow.

### HTML

```html
<section class="layout-pricing">
  <header class="slide-header">
    <h2 class="slide-heading">Simple, transparent pricing</h2>
    <p class="slide-subheading">No surprise fees. Cancel any time.</p>
  </header>

  <div class="pricing-grid">
    <!-- Starter tier -->
    <div class="pricing-card">
      <span class="pricing-tier">Starter</span>
      <div class="pricing-price">$0<span class="pricing-period">/mo</span></div>
      <p class="pricing-tagline">For individuals exploring the platform.</p>
      <ul class="pricing-features">
        <li>1 workspace</li>
        <li>Up to 3 projects</li>
        <li>Community support</li>
        <li>Core token sync</li>
      </ul>
      <a href="#" class="pricing-cta pricing-cta--outline">Get started free</a>
    </div>

    <!-- Pro tier (featured) -->
    <div class="pricing-card pricing-card--featured">
      <span class="pricing-tier">Pro</span>
      <div class="pricing-price">$49<span class="pricing-period">/mo</span></div>
      <p class="pricing-tagline">For growing product teams.</p>
      <ul class="pricing-features">
        <li>Unlimited workspaces</li>
        <li>Unlimited projects</li>
        <li>Priority support</li>
        <li>Full token sync + versioning</li>
        <li>GitHub &amp; Figma integration</li>
      </ul>
      <a href="#" class="pricing-cta pricing-cta--solid">Start free trial</a>
    </div>

    <!-- Enterprise tier -->
    <div class="pricing-card">
      <span class="pricing-tier">Enterprise</span>
      <div class="pricing-price">Custom</div>
      <p class="pricing-tagline">For large organisations with advanced needs.</p>
      <ul class="pricing-features">
        <li>Everything in Pro</li>
        <li>SSO &amp; SCIM provisioning</li>
        <li>Dedicated CSM</li>
        <li>SLA &amp; compliance docs</li>
        <li>On-premise deployment option</li>
      </ul>
      <a href="#" class="pricing-cta pricing-cta--outline">Contact sales</a>
    </div>
  </div>
</section>
```

### CSS

```css
/* ── Pricing Table ────────────────────────────────────────────────── */
.layout-pricing {
  justify-content: flex-start;
  gap: var(--space-5);
}

.pricing-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  width: 100%;
  min-width: 0;
  align-items: center;
}

.pricing-card {
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
  padding: 1.75rem 1.5rem;
  border-radius: 1rem;
  border: 2px solid var(--color-border);
  background: var(--color-surface);
  box-sizing: border-box;
  min-width: 0;
  overflow: hidden;
  overflow-wrap: break-word;
}

.pricing-card--featured {
  border-color: var(--color-primary);
  background: color-mix(in srgb, var(--color-primary) 5%, var(--color-background));
  transform: scale(1.03);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.10);
  position: relative;
  z-index: 1;
}

.pricing-tier {
  font-size: var(--type-label);
  font-weight: var(--fw-bold);
  text-transform: uppercase;
  letter-spacing: var(--ls-wider);
  color: var(--color-primary);
}

.pricing-price {
  font-size: var(--type-kpi-number);
  font-weight: var(--fw-extrabold);
  line-height: var(--lh-tight);
  color: var(--color-text-primary);
}

.pricing-period {
  font-size: var(--type-body);
  font-weight: var(--fw-medium);
  color: var(--color-text-secondary);
}

.pricing-tagline {
  font-size: var(--type-body-sm);
  color: var(--color-text-secondary);
  margin: 0;
  line-height: var(--lh-snug);
}

.pricing-features {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
  flex: 1;
}

.pricing-features li {
  font-size: var(--type-body-sm);
  color: var(--color-text-secondary);
  padding-left: var(--space-5);
  position: relative;
  line-height: var(--lh-snug);
}

/* Checkmark pseudo-element */
.pricing-features li::before {
  content: "✓";
  position: absolute;
  left: 0;
  color: var(--color-success);
  font-weight: var(--fw-bold);
}

.pricing-cta {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.625rem 1.25rem;
  border-radius: 0.5rem;
  font-size: var(--type-body-sm);
  font-weight: var(--fw-semibold);
  text-decoration: none;
  text-align: center;
  transition: opacity 0.15s ease;
}

.pricing-cta--solid {
  background: var(--color-primary);
  color: white;
  border: 2px solid var(--color-primary);
}

.pricing-cta--outline {
  background: transparent;
  color: var(--color-primary);
  border: 2px solid var(--color-primary);
}
```

---

## 14. Before / After (`.layout-before-after`)

Full-bleed split screen with no internal padding between panes. Left pane shows the "before" state; right pane shows the "after" state with a tinted accent background.

### HTML

```html
<section class="layout-before-after">
  <div class="before-pane">
    <span class="pane-label pane-label--before">Before</span>
    <h3 class="pane-heading">Fragmented toolchain</h3>
    <ul class="pane-list">
      <li>Figma for design mockups</li>
      <li>Zeplin for developer specs</li>
      <li>Storybook maintained separately</li>
      <li>Notion for design decisions</li>
      <li>Slack DMs for handoff notes</li>
    </ul>
    <p class="pane-outcome pane-outcome--negative">Result: 3-week design-to-dev cycle</p>
  </div>

  <div class="after-pane">
    <span class="pane-label pane-label--after">After</span>
    <h3 class="pane-heading">Unified platform</h3>
    <ul class="pane-list pane-list--check">
      <li>Design + code in one canvas</li>
      <li>Auto-generated component specs</li>
      <li>Storybook synced from tokens</li>
      <li>Decisions tracked in-context</li>
      <li>One-click PR creation</li>
    </ul>
    <p class="pane-outcome pane-outcome--positive">Result: 4-day design-to-dev cycle</p>
  </div>
</section>
```

### CSS

```css
/* ── Before / After ───────────────────────────────────────────────── */
.layout-before-after {
  display: grid !important;
  flex-direction: row;
  grid-template-columns: 1fr 1fr;
  gap: 0;
  padding: 0 !important;
  overflow: hidden;
  justify-content: flex-start;
}

.before-pane {
  background: var(--color-surface);
  border-right: 3px solid var(--color-border);
  padding: 3rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: var(--space-4);
  min-width: 0;
  overflow: hidden;
  overflow-wrap: break-word;
}

.after-pane {
  background: color-mix(in srgb, var(--color-primary) 6%, var(--color-background));
  padding: 3rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: var(--space-4);
  min-width: 0;
  overflow: hidden;
  overflow-wrap: break-word;
}

.pane-label {
  font-size: var(--type-label);
  font-weight: var(--fw-bold);
  letter-spacing: var(--ls-wider);
  text-transform: uppercase;
}

.pane-label--before {
  color: var(--color-text-secondary);
}

.pane-label--after {
  color: var(--color-primary);
}

.pane-heading {
  font-size: var(--type-subheading);
  font-weight: var(--fw-bold);
  line-height: var(--lh-snug);
  color: var(--color-text-primary);
  margin: 0;
}

.pane-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
  flex: 1;
}

.pane-list li {
  font-size: var(--type-body-sm);
  color: var(--color-text-secondary);
  line-height: var(--lh-snug);
  padding-left: var(--space-4);
  position: relative;
}

.pane-list li::before {
  content: "–";
  position: absolute;
  left: 0;
  color: var(--color-border);
}

.pane-list--check li::before {
  content: "✓";
  color: var(--color-success);
  font-weight: var(--fw-bold);
}

.pane-outcome {
  font-size: var(--type-body-sm);
  font-weight: var(--fw-semibold);
  margin: 0;
  padding: 0.5rem 0.75rem;
  border-radius: 0.375rem;
}

.pane-outcome--negative {
  background: color-mix(in srgb, var(--color-danger) 10%, var(--color-background));
  color: var(--color-danger);
}

.pane-outcome--positive {
  background: color-mix(in srgb, var(--color-success) 10%, var(--color-background));
  color: var(--color-success);
}
```

---

## 15. Agenda / TOC (`.layout-agenda`)

Numbered list of agenda items, each with a title and optional time estimate. Active items are highlighted with a primary-colored left border and surface background.

### HTML

```html
<section class="layout-agenda">
  <header class="slide-header">
    <h2 class="slide-heading">Today's agenda</h2>
  </header>

  <ul class="agenda-list" role="list">
    <li class="agenda-item active" aria-current="true">
      <span class="agenda-num">01</span>
      <span class="agenda-title">Company overview &amp; mission</span>
      <span class="agenda-time">5 min</span>
    </li>
    <li class="agenda-item">
      <span class="agenda-num">02</span>
      <span class="agenda-title">Market opportunity</span>
      <span class="agenda-time">10 min</span>
    </li>
    <li class="agenda-item">
      <span class="agenda-num">03</span>
      <span class="agenda-title">Product demo</span>
      <span class="agenda-time">15 min</span>
    </li>
    <li class="agenda-item">
      <span class="agenda-num">04</span>
      <span class="agenda-title">Business model &amp; traction</span>
      <span class="agenda-time">10 min</span>
    </li>
    <li class="agenda-item">
      <span class="agenda-num">05</span>
      <span class="agenda-title">Team &amp; roadmap</span>
      <span class="agenda-time">5 min</span>
    </li>
    <li class="agenda-item">
      <span class="agenda-num">06</span>
      <span class="agenda-title">Q&amp;A</span>
      <span class="agenda-time">15 min</span>
    </li>
  </ul>
</section>
```

### CSS

```css
/* ── Agenda / TOC ─────────────────────────────────────────────────── */
.layout-agenda {
  justify-content: flex-start;
  gap: var(--space-5);
}

.agenda-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
  width: 100%;
  min-width: 0;
}

.agenda-item {
  display: grid;
  grid-template-columns: 3rem 1fr auto;
  gap: var(--space-4);
  align-items: center;
  padding: var(--space-4) var(--space-6);
  border-radius: 0.5rem;
  border-left: 4px solid transparent;
  transition: background 0.15s ease, border-color 0.15s ease;
  min-width: 0;
  overflow-wrap: break-word;
}

.agenda-item.active {
  background: var(--color-surface);
  border-left-color: var(--color-primary);
}

.agenda-num {
  font-size: var(--type-body-sm);
  font-weight: var(--fw-bold);
  color: var(--color-primary);
  line-height: 1;
  font-variant-numeric: tabular-nums;
}

.agenda-title {
  font-size: var(--type-body);
  font-weight: var(--fw-medium);
  color: var(--color-text-primary);
  line-height: var(--lh-snug);
}

.agenda-item:not(.active) .agenda-title {
  color: var(--color-text-secondary);
}

.agenda-time {
  font-size: var(--type-caption);
  color: var(--color-text-secondary);
  white-space: nowrap;
  font-variant-numeric: tabular-nums;
}
```

---

## Token Reference Summary

All tokens consumed across these 15 layouts. Exact values are defined in the design system token file.

| Category | Tokens Used |
|---|---|
| Color | `--color-primary`, `--color-secondary`, `--color-success`, `--color-warning`, `--color-danger`, `--color-background`, `--color-surface`, `--color-surface-raised`, `--color-border`, `--color-text-primary`, `--color-text-secondary`, `--color-link` |
| Typography size | `--type-slide-title`, `--type-slide-heading`, `--type-section-title`, `--type-subheading`, `--type-body`, `--type-body-sm`, `--type-caption`, `--type-label`, `--type-kpi-number`, `--type-code` |
| Font weight | `--fw-extrabold`, `--fw-bold`, `--fw-semibold`, `--fw-medium` |
| Line height | `--lh-tight`, `--lh-snug`, `--lh-normal`, `--lh-relaxed` |
| Letter spacing | `--ls-tighter`, `--ls-tight`, `--ls-wide`, `--ls-wider`, `--ls-normal` |
| Spacing | `--space-1` through `--space-8` |
| Gap | `--gap-sm`, `--gap-md`, `--gap-xl` |
