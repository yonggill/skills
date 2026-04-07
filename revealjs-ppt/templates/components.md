# Reusable Components Reference

All CSS properties must use `var()` references to design system tokens. Never use hardcoded colors, sizes, or spacing values. Token categories: `--color-*`, `--type-*`, `--space-*`, `--fw-*`, `--lh-*`, `--ls-*`, `--gap-*`.

---

## 1. KPI Card (`.kpi-card`)

Displays a key performance indicator with an icon, large number, descriptive label, and optional delta indicator.

### HTML

```html
<div class="kpi-card">
  <div class="kpi-icon">📈</div>
  <div class="kpi-number">$4.2M</div>
  <div class="kpi-label">Annual Recurring Revenue</div>
  <div class="kpi-delta kpi-delta--up">▲ 18% vs last quarter</div>
</div>
```

**Delta down variant:**

```html
<div class="kpi-delta kpi-delta--down">▼ 3% vs last quarter</div>
```

### CSS

```css
/* ── KPI Card ─────────────────────────────────────────────────────── */
.kpi-card {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: 0.75rem;
  padding: 1.5rem;
  overflow: hidden;
}

/* 4px top accent bar */
.kpi-card::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: var(--color-primary);
  border-radius: 0.75rem 0.75rem 0 0;
}

.kpi-icon {
  font-size: 2rem;
  line-height: 1;
}

.kpi-number {
  font-size: var(--type-kpi-number);
  font-weight: var(--fw-extrabold);
  line-height: var(--lh-tight);
  letter-spacing: var(--ls-tighter);
  color: var(--color-text-primary);
}

.kpi-label {
  font-size: var(--type-caption);
  font-weight: var(--fw-semibold);
  text-transform: uppercase;
  letter-spacing: var(--ls-wide);
  color: var(--color-text-secondary);
}

.kpi-delta {
  font-size: var(--type-caption);
  font-weight: var(--fw-semibold);
}

.kpi-delta--up {
  color: var(--color-success);
}

.kpi-delta--down {
  color: var(--color-danger);
}
```

---

## 2. Feature Card (`.feature-card`)

Highlights a product feature or benefit with an icon, title, and short description.

### HTML

```html
<div class="feature-card">
  <div class="feature-icon-wrap">
    <svg class="feature-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <!-- replace with appropriate icon path -->
      <path d="M12 2L2 7l10 5 10-5-10-5z"/>
      <path d="M2 17l10 5 10-5"/>
      <path d="M2 12l10 5 10-5"/>
    </svg>
  </div>
  <h3 class="feature-title">Multi-Cloud Support</h3>
  <p class="feature-desc">Deploy seamlessly across AWS, Azure, and GCP with a single unified control plane.</p>
</div>
```

### CSS

```css
/* ── Feature Card ─────────────────────────────────────────────────── */
.feature-card {
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: 0.75rem;
  padding: 1.5rem;
}

.feature-icon-wrap {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  border-radius: 0.5rem;
  background: color-mix(in srgb, var(--color-primary) 12%, white);
  flex-shrink: 0;
}

.feature-icon {
  width: 24px;
  height: 24px;
  color: var(--color-primary);
}

.feature-title {
  font-size: var(--type-subheading);
  font-weight: var(--fw-semibold);
  line-height: var(--lh-snug);
  color: var(--color-text-primary);
  margin: 0;
}

.feature-desc {
  font-size: var(--type-body-sm);
  line-height: var(--lh-relaxed);
  color: var(--color-text-secondary);
  margin: 0;
}
```

---

## 3. Quote Block (`.quote-component`)

Renders a styled pull quote with author attribution and optional source.

### HTML

```html
<blockquote class="quote-component">
  <p class="quote-component__text">
    "The only way to do great work is to love what you do. If you haven't found it yet, keep looking."
  </p>
  <footer class="quote-component__footer">
    <cite class="quote-component__author">Steve Jobs</cite>
    <span class="quote-component__source">Stanford Commencement Address, 2005</span>
  </footer>
</blockquote>
```

### CSS

```css
/* ── Quote Block ──────────────────────────────────────────────────── */
.quote-component {
  border-left: 5px solid var(--color-primary);
  padding: 1.25rem 1.5rem;
  background: color-mix(in srgb, var(--color-primary) 5%, white);
  border-radius: 0 0.5rem 0.5rem 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}

.quote-component__text {
  font-size: var(--type-body);
  line-height: var(--lh-relaxed);
  font-style: italic;
  color: var(--color-text-primary);
  margin: 0;
}

.quote-component__footer {
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
}

.quote-component__author {
  font-size: var(--type-body-sm);
  font-weight: var(--fw-semibold);
  font-style: normal;
  color: var(--color-text-primary);
}

.quote-component__source {
  font-size: var(--type-caption);
  color: var(--color-text-secondary);
}
```

---

## 4. Image with Caption (`.img-caption`)

Wraps an image in a semantic `figure` element with a styled caption beneath it.

### HTML

```html
<figure class="img-caption">
  <img
    class="img-caption__img"
    src="path/to/image.jpg"
    alt="Descriptive alt text for the image"
    width="800"
    height="450"
  />
  <figcaption class="img-caption__text">
    Figure 1: Global market share distribution by region, Q4 2025.
  </figcaption>
</figure>
```

### CSS

```css
/* ── Image with Caption ───────────────────────────────────────────── */
.img-caption {
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
  margin: 0;
}

.img-caption__img {
  width: 100%;
  height: auto;
  border-radius: 0.5rem;
  object-fit: cover;
  border: 1px solid var(--color-border);
  display: block;
}

.img-caption__text {
  font-size: var(--type-caption);
  line-height: var(--lh-normal);
  color: var(--color-text-secondary);
  text-align: center;
}
```

---

## 5. Numbered List (`.icon-list`)

An ordered list where each item has a numbered circle badge, a bold title, and supporting body text.

### HTML

```html
<ol class="icon-list">
  <li class="icon-list__item">
    <span class="icon-list__num" aria-hidden="true">1</span>
    <div class="icon-list__content">
      <strong class="icon-list__title">Define the Problem Space</strong>
      <p class="icon-list__body">Conduct stakeholder interviews and competitive analysis to surface unmet needs.</p>
    </div>
  </li>
  <li class="icon-list__item">
    <span class="icon-list__num" aria-hidden="true">2</span>
    <div class="icon-list__content">
      <strong class="icon-list__title">Prototype and Validate</strong>
      <p class="icon-list__body">Build low-fidelity wireframes and run usability tests with real users.</p>
    </div>
  </li>
  <li class="icon-list__item">
    <span class="icon-list__num" aria-hidden="true">3</span>
    <div class="icon-list__content">
      <strong class="icon-list__title">Ship and Iterate</strong>
      <p class="icon-list__body">Launch the MVP to a beta cohort, measure outcomes, and refine continuously.</p>
    </div>
  </li>
</ol>
```

### CSS

```css
/* ── Numbered List ────────────────────────────────────────────────── */
.icon-list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-5);
}

.icon-list__item {
  display: flex;
  align-items: flex-start;
  gap: var(--space-4);
}

.icon-list__num {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 2rem;
  height: 2rem;
  border-radius: 50%;
  background: var(--color-primary);
  color: white;
  font-weight: var(--fw-bold);
  font-size: var(--type-caption);
  flex-shrink: 0;
  line-height: 1;
}

.icon-list__content {
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
}

.icon-list__title {
  font-size: var(--type-body-sm);
  font-weight: var(--fw-semibold);
  color: var(--color-text-primary);
  display: block;
}

.icon-list__body {
  font-size: var(--type-caption);
  line-height: var(--lh-relaxed);
  color: var(--color-text-secondary);
  margin: 0;
}
```

---

## 6. Progress / Metric Bar (`.metric-bar`)

Visualises a percentage-based metric with a label, value, and animated progress track. Set the fill width via inline style.

### HTML

```html
<!-- Standard variant -->
<div class="metric-bar">
  <div class="metric-bar__header">
    <span class="metric-bar__label">Customer Satisfaction</span>
    <span class="metric-bar__value">92%</span>
  </div>
  <div class="metric-bar__track" role="progressbar" aria-valuenow="92" aria-valuemin="0" aria-valuemax="100" aria-label="Customer Satisfaction 92%">
    <div class="metric-bar__fill" style="width: 92%;"></div>
  </div>
</div>

<!-- Gradient variant -->
<div class="metric-bar">
  <div class="metric-bar__header">
    <span class="metric-bar__label">Revenue Growth</span>
    <span class="metric-bar__value">78%</span>
  </div>
  <div class="metric-bar__track" role="progressbar" aria-valuenow="78" aria-valuemin="0" aria-valuemax="100" aria-label="Revenue Growth 78%">
    <div class="metric-bar__fill metric-bar__fill--gradient" style="width: 78%;"></div>
  </div>
</div>
```

### CSS

```css
/* ── Progress / Metric Bar ────────────────────────────────────────── */
.metric-bar {
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
}

.metric-bar__header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
}

.metric-bar__label {
  font-size: var(--type-body-sm);
  font-weight: var(--fw-medium);
  color: var(--color-text-primary);
}

.metric-bar__value {
  font-size: var(--type-body-sm);
  font-weight: var(--fw-bold);
  color: var(--color-primary);
}

.metric-bar__track {
  height: 10px;
  background: var(--color-surface-raised);
  border-radius: 9999px;
  overflow: hidden;
}

.metric-bar__fill {
  height: 100%;
  background: var(--color-primary);
  border-radius: 9999px;
  transition: width 0.8s ease-in-out;
}

/* Gradient variant */
.metric-bar__fill--gradient {
  background: linear-gradient(
    to right,
    var(--color-primary),
    var(--color-secondary)
  );
}
```

---

## 7. Badge / Tag (`.badge`)

Compact inline label used for statuses, categories, or tags. Apply one variant modifier class alongside `.badge`.

### HTML

```html
<!-- Tinted variants -->
<span class="badge badge--primary">New</span>
<span class="badge badge--success">Active</span>
<span class="badge badge--warning">Pending</span>
<span class="badge badge--danger">Deprecated</span>
<span class="badge badge--neutral">Draft</span>

<!-- Solid filled variant -->
<span class="badge badge--solid-primary">Featured</span>
```

### CSS

```css
/* ── Badge / Tag ──────────────────────────────────────────────────── */
.badge {
  display: inline-flex;
  align-items: center;
  padding: 0.2em 0.65em;
  border-radius: 9999px;
  font-size: var(--type-label);
  font-weight: var(--fw-semibold);
  letter-spacing: var(--ls-wide);
  text-transform: uppercase;
  line-height: 1;
  white-space: nowrap;
}

/* Tinted variants — 15% color saturation on white base */
.badge--primary {
  background: color-mix(in srgb, var(--color-primary) 15%, white);
  color: var(--color-primary);
}

.badge--success {
  background: color-mix(in srgb, var(--color-success) 15%, white);
  color: var(--color-success);
}

.badge--warning {
  background: color-mix(in srgb, var(--color-warning) 15%, white);
  color: var(--color-warning);
}

.badge--danger {
  background: color-mix(in srgb, var(--color-danger) 15%, white);
  color: var(--color-danger);
}

.badge--neutral {
  background: color-mix(in srgb, var(--color-neutral) 15%, white);
  color: var(--color-neutral);
}

/* Solid filled variant */
.badge--solid-primary {
  background: var(--color-primary);
  color: white;
}
```

---

## 8. Callout Box (`.callout`)

Draws attention to important information using a colour-coded side border and tinted background. Apply one variant modifier alongside `.callout`.

### HTML

```html
<!-- Info callout -->
<div class="callout callout--info">
  <div class="callout__icon" aria-hidden="true">ℹ️</div>
  <div class="callout__body">
    <strong class="callout__title">Note</strong>
    <p class="callout__text">This feature requires API version 3.0 or higher. Check your integration docs before upgrading.</p>
  </div>
</div>

<!-- Success callout -->
<div class="callout callout--success">
  <div class="callout__icon" aria-hidden="true">✅</div>
  <div class="callout__body">
    <strong class="callout__title">Complete</strong>
    <p class="callout__text">All validation checks passed. You are ready to deploy to production.</p>
  </div>
</div>

<!-- Warning callout -->
<div class="callout callout--warning">
  <div class="callout__icon" aria-hidden="true">⚠️</div>
  <div class="callout__body">
    <strong class="callout__title">Warning</strong>
    <p class="callout__text">Proceeding will reset all user preferences. This action cannot be undone.</p>
  </div>
</div>

<!-- Danger callout -->
<div class="callout callout--danger">
  <div class="callout__icon" aria-hidden="true">🚫</div>
  <div class="callout__body">
    <strong class="callout__title">Critical</strong>
    <p class="callout__text">Service outage detected in us-east-1. Failover is in progress.</p>
  </div>
</div>
```

### CSS

```css
/* ── Callout Box ──────────────────────────────────────────────────── */
.callout {
  display: flex;
  align-items: flex-start;
  gap: var(--space-4);
  padding: 1rem 1.25rem;
  border-radius: 0.5rem;
  border-left: 5px solid;
}

.callout__icon {
  font-size: 1.25rem;
  line-height: 1;
  flex-shrink: 0;
  margin-top: 0.1em;
}

.callout__body {
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
}

.callout__title {
  font-size: var(--type-body-sm);
  font-weight: var(--fw-semibold);
  color: var(--color-text-primary);
  display: block;
}

.callout__text {
  font-size: var(--type-body-sm);
  line-height: var(--lh-relaxed);
  color: var(--color-text-secondary);
  margin: 0;
}

/* Variant: info — uses --color-secondary */
.callout--info {
  background: color-mix(in srgb, var(--color-secondary) 10%, white);
  border-color: var(--color-secondary);
}

/* Variant: success */
.callout--success {
  background: color-mix(in srgb, var(--color-success) 10%, white);
  border-color: var(--color-success);
}

/* Variant: warning */
.callout--warning {
  background: color-mix(in srgb, var(--color-warning) 10%, white);
  border-color: var(--color-warning);
}

/* Variant: danger */
.callout--danger {
  background: color-mix(in srgb, var(--color-danger) 10%, white);
  border-color: var(--color-danger);
}
```

---

## 9. Icon Grid (`.icon-grid`)

Displays a collection of icons with labels in a uniform grid. Apply one column count modifier alongside `.icon-grid`.

### HTML

```html
<!-- 3-column grid -->
<div class="icon-grid icon-grid--3col">
  <div class="icon-grid__item">
    <div class="icon-grid__icon">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
        <path d="M12 2L2 7l10 5 10-5-10-5z"/>
      </svg>
    </div>
    <span class="icon-grid__label">Infrastructure</span>
  </div>
  <div class="icon-grid__item">
    <div class="icon-grid__icon">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
        <circle cx="12" cy="12" r="10"/>
        <path d="M12 8v4l3 3"/>
      </svg>
    </div>
    <span class="icon-grid__label">Uptime</span>
  </div>
  <div class="icon-grid__item">
    <div class="icon-grid__icon">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
        <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/>
      </svg>
    </div>
    <span class="icon-grid__label">Security</span>
  </div>
</div>

<!-- 4-column grid — add more .icon-grid__item elements as needed -->
<div class="icon-grid icon-grid--4col">
  <!-- .icon-grid__item × 4 -->
</div>

<!-- 5-column grid -->
<div class="icon-grid icon-grid--5col">
  <!-- .icon-grid__item × 5 -->
</div>
```

### CSS

```css
/* ── Icon Grid ────────────────────────────────────────────────────── */
.icon-grid {
  display: grid;
  gap: var(--gap-grid);
}

/* Column count modifiers */
.icon-grid--3col {
  grid-template-columns: repeat(3, 1fr);
}

.icon-grid--4col {
  grid-template-columns: repeat(4, 1fr);
}

.icon-grid--5col {
  grid-template-columns: repeat(5, 1fr);
}

.icon-grid__item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: var(--space-3);
  padding: 1.25rem 1rem;
  border-radius: 0.75rem;
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  text-align: center;
}

.icon-grid__icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  border-radius: 0.5rem;
  background: color-mix(in srgb, var(--color-primary) 12%, white);
  flex-shrink: 0;
}

.icon-grid__icon svg {
  width: 24px;
  height: 24px;
  color: var(--color-primary);
}

.icon-grid__label {
  font-size: var(--type-caption);
  font-weight: var(--fw-semibold);
  color: var(--color-text-primary);
  letter-spacing: var(--ls-normal);
  line-height: var(--lh-snug);
}
```

---

## Token Reference Summary

The table below lists every token category consumed by these components. Exact values are defined in the design system token file and are not duplicated here.

| Category | Tokens Used |
|---|---|
| Color | `--color-primary`, `--color-secondary`, `--color-success`, `--color-warning`, `--color-danger`, `--color-neutral`, `--color-surface`, `--color-surface-raised`, `--color-border`, `--color-text-primary`, `--color-text-secondary` |
| Typography size | `--type-kpi-number`, `--type-subheading`, `--type-body`, `--type-body-sm`, `--type-caption`, `--type-label` |
| Font weight | `--fw-extrabold`, `--fw-bold`, `--fw-semibold`, `--fw-medium` |
| Line height | `--lh-tight`, `--lh-snug`, `--lh-normal`, `--lh-relaxed` |
| Letter spacing | `--ls-tighter`, `--ls-wide`, `--ls-normal` |
| Spacing | `--space-1`, `--space-2`, `--space-3`, `--space-4`, `--space-5` |
| Gap | `--gap-grid` |
