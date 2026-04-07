# reveal.js API Reference (v4.6.1)

This document is a complete technical reference for generating valid reveal.js HTML presentations. All URLs, attributes, class names, and configuration options are exact and production-ready.

---

## 1. CDN URLs

### reveal.js v4.6.1 (unpkg)

#### Core CSS

```
https://unpkg.com/reveal.js@4.6.1/dist/reset.css
https://unpkg.com/reveal.js@4.6.1/dist/reveal.css
```

#### Theme CSS (use one)

```
https://unpkg.com/reveal.js@4.6.1/dist/theme/black.css
https://unpkg.com/reveal.js@4.6.1/dist/theme/white.css
https://unpkg.com/reveal.js@4.6.1/dist/theme/league.css
https://unpkg.com/reveal.js@4.6.1/dist/theme/beige.css
https://unpkg.com/reveal.js@4.6.1/dist/theme/night.css
https://unpkg.com/reveal.js@4.6.1/dist/theme/serif.css
https://unpkg.com/reveal.js@4.6.1/dist/theme/simple.css
https://unpkg.com/reveal.js@4.6.1/dist/theme/solarized.css
https://unpkg.com/reveal.js@4.6.1/dist/theme/moon.css
https://unpkg.com/reveal.js@4.6.1/dist/theme/dracula.css
https://unpkg.com/reveal.js@4.6.1/dist/theme/sky.css
https://unpkg.com/reveal.js@4.6.1/dist/theme/blood.css
```

#### Highlight.js Themes

```
https://unpkg.com/reveal.js@4.6.1/plugin/highlight/monokai.css
https://unpkg.com/reveal.js@4.6.1/plugin/highlight/zenburn.css
```

#### Core JS

```
https://unpkg.com/reveal.js@4.6.1/dist/reveal.js
```

#### Plugin JS

```
https://unpkg.com/reveal.js@4.6.1/plugin/zoom/zoom.js
https://unpkg.com/reveal.js@4.6.1/plugin/notes/notes.js
https://unpkg.com/reveal.js@4.6.1/plugin/search/search.js
https://unpkg.com/reveal.js@4.6.1/plugin/markdown/markdown.js
https://unpkg.com/reveal.js@4.6.1/plugin/highlight/highlight.js
https://unpkg.com/reveal.js@4.6.1/plugin/math/math.js
```

---

### reveal.js v5.2.1 (cdnjs — alternative CDN)

#### Core CSS

```
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/reset.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/reveal.min.css
```

#### Theme CSS (use one)

```
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/black.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/white.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/league.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/beige.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/night.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/serif.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/simple.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/solarized.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/moon.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/dracula.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/sky.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/blood.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/black-contrast.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/theme/white-contrast.min.css
```

#### Core JS

```
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/reveal.min.js
```

#### Plugin JS

```
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/plugin/zoom/zoom.min.js
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/plugin/notes/notes.min.js
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/plugin/search/search.min.js
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/plugin/markdown/markdown.min.js
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/plugin/highlight/highlight.min.js
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/5.2.1/plugin/math/math.min.js
```

---

## 2. HTML Structure

### Minimal Valid Document

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title>Presentation Title</title>
    <link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/dist/reset.css" />
    <link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/dist/reveal.css" />
    <link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/dist/theme/black.css" />
  </head>
  <body>
    <div class="reveal">
      <div class="slides">
        <section>Slide 1</section>
        <section>Slide 2</section>
      </div>
    </div>
    <script src="https://unpkg.com/reveal.js@4.6.1/dist/reveal.js"></script>
    <script>
      Reveal.initialize();
    </script>
  </body>
</html>
```

### Element Hierarchy

```
<div class="reveal">          ← Required root element
  <div class="slides">        ← Required slides container
    <section>...</section>    ← Horizontal slide
    <section>               ← Horizontal slide with vertical children
      <section>...</section> ← Vertical slide (child)
      <section>...</section> ← Vertical slide (child)
    </section>
  </div>
</div>
```

### Vertical (Nested) Slides

```html
<section>
  <!-- This outer section becomes a "column" -->
  <section>First vertical slide</section>
  <section>Second vertical slide</section>
  <section>Third vertical slide</section>
</section>
```

### Slide ID for URL Navigation

```html
<!-- Navigable via URL #/my-slide -->
<section id="my-slide">
  <h2>Named Slide</h2>
</section>

<!-- Vertical slide navigable via URL #/column/my-subsection -->
<section id="column">
  <section id="my-subsection">Vertical named slide</section>
</section>
```

### data-state Attribute

Adds the specified class to the `.reveal` element when the slide becomes active. Use for triggering CSS animations or JavaScript events.

```html
<section data-state="my-custom-state">
  This slide applies class "my-custom-state" to .reveal
</section>
```

```javascript
// Listen for state change
Reveal.on('my-custom-state', function () {
  // triggered when the slide with data-state="my-custom-state" is shown
});
```

### data-visibility Attribute

```html
<!-- Slide is hidden but still counts in the navigation index -->
<section data-visibility="hidden">
  This slide is skipped during navigation
</section>

<!-- Slide is hidden and does NOT count in slide numbering -->
<section data-visibility="uncounted">
  This slide is skipped and not counted
</section>
```

---

## 3. Configuration Options

All options are passed as an object to `Reveal.initialize({})`. Options not specified use their defaults.

### Display and UI

| Option | Default | Type | Description |
|---|---|---|---|
| `controls` | `true` | boolean | Show arrow navigation controls |
| `controlsTutorial` | `true` | boolean | Show tutorial arrows on first visit |
| `controlsLayout` | `'bottom-right'` | string | Position: `'bottom-right'`, `'edges'` |
| `controlsBackArrows` | `'faded'` | string | Style when navigating back: `'faded'`, `'hidden'`, `'visible'` |
| `progress` | `true` | boolean | Show a progress bar at the bottom |
| `slideNumber` | `false` | boolean/string | Show slide number. Formats: `'h.v'`, `'h/v'`, `'c'`, `'c/t'` |
| `showSlideNumber` | `'all'` | string | When to show slide numbers: `'all'`, `'print'`, `'speaker'` |
| `center` | `true` | boolean | Vertically center slide content |
| `help` | `true` | boolean | Show `?` keyboard shortcut help overlay |
| `pause` | `true` | boolean | Allow pausing the presentation (press `B` or `.`) |
| `showNotes` | `false` | boolean | Show speaker notes in the slide view |
| `hideInactiveCursor` | `true` | boolean | Hide mouse cursor after inactivity |
| `hideCursorTime` | `5000` | number | Milliseconds before cursor is hidden |
| `disableLayout` | `false` | boolean | Disable slide scaling; use raw CSS layout |

### Navigation

| Option | Default | Type | Description |
|---|---|---|---|
| `hash` | `false` | boolean | Update the browser URL hash on slide change |
| `hashOneBasedIndex` | `false` | boolean | Use 1-based indices in URL hash |
| `respondToHashChanges` | `true` | boolean | React to URL hash changes |
| `history` | `false` | boolean | Push slide changes to browser history |
| `keyboard` | `true` | boolean | Enable keyboard navigation |
| `overview` | `true` | boolean | Enable slide overview mode (press `O` or `Esc`) |
| `touch` | `true` | boolean | Enable touch/swipe navigation |
| `loop` | `false` | boolean | Loop the presentation |
| `rtl` | `false` | boolean | Right-to-left navigation direction |
| `navigationMode` | `'default'` | string | Navigation behavior: `'default'`, `'linear'`, `'grid'` |
| `shuffle` | `false` | boolean | Shuffle slides randomly on each load |
| `fragments` | `true` | boolean | Enable fragment animations |
| `fragmentInURL` | `true` | boolean | Include fragment index in URL hash |
| `jumpToSlide` | `true` | boolean | Allow jumping to a slide by typing its number |
| `mouseWheel` | `false` | boolean | Navigate with mouse wheel |
| `previewLinks` | `false` | boolean | Open links in an iframe preview overlay |

### Transitions

| Option | Default | Type | Description |
|---|---|---|---|
| `transition` | `'slide'` | string | Default slide transition: `'none'`, `'fade'`, `'slide'`, `'convex'`, `'concave'`, `'zoom'` |
| `transitionSpeed` | `'default'` | string | Transition speed: `'default'`, `'fast'`, `'slow'` |
| `backgroundTransition` | `'fade'` | string | Background transition: `'none'`, `'fade'`, `'slide'`, `'convex'`, `'concave'`, `'zoom'` |

### Auto-Animate

| Option | Default | Type | Description |
|---|---|---|---|
| `autoAnimate` | `true` | boolean | Enable auto-animate between matching slides |
| `autoAnimateEasing` | `'ease'` | string | CSS easing function for auto-animate |
| `autoAnimateDuration` | `1.0` | number | Duration in seconds for auto-animate |
| `autoAnimateUnmatched` | `true` | boolean | Animate unmatched elements with a fade |

### Size and Scale

| Option | Default | Type | Description |
|---|---|---|---|
| `width` | `960` | number | Presentation width in pixels |
| `height` | `700` | number | Presentation height in pixels |
| `margin` | `0.04` | number | Margin around slides as a fraction (0–1) |
| `minScale` | `0.2` | number | Minimum scale factor for responsive scaling |
| `maxScale` | `2.0` | number | Maximum scale factor for responsive scaling |

### Media

| Option | Default | Type | Description |
|---|---|---|---|
| `autoPlayMedia` | `null` | boolean/null | Auto-play embedded media: `null` = play only when visible |
| `preloadIframes` | `null` | boolean/null | Pre-load iframe content: `null` = load only when visible |
| `viewDistance` | `3` | number | Number of slides away to pre-load |
| `mobileViewDistance` | `2` | number | `viewDistance` override for mobile devices |

### PDF Export

| Option | Default | Type | Description |
|---|---|---|---|
| `pdfMaxPagesPerSlide` | `Infinity` | number | Maximum PDF pages per slide |
| `pdfSeparateFragments` | `true` | boolean | Each fragment state becomes a separate PDF page |

### Complete Initialization Example

```html
<script>
  Reveal.initialize({
    // Display
    controls: true,
    controlsLayout: 'bottom-right',
    progress: true,
    slideNumber: 'c/t',
    center: true,
    help: true,

    // Navigation
    hash: true,
    history: true,
    keyboard: true,
    overview: true,
    touch: true,
    loop: false,
    navigationMode: 'default',
    fragments: true,
    mouseWheel: false,

    // Transitions
    transition: 'slide',
    transitionSpeed: 'default',
    backgroundTransition: 'fade',

    // Auto-animate
    autoAnimate: true,
    autoAnimateEasing: 'ease',
    autoAnimateDuration: 1.0,
    autoAnimateUnmatched: true,

    // Size
    width: 960,
    height: 700,
    margin: 0.04,
    minScale: 0.2,
    maxScale: 2.0,

    // Media
    autoPlayMedia: null,
    preloadIframes: null,
    viewDistance: 3,
    mobileViewDistance: 2,

    // PDF
    pdfMaxPagesPerSlide: 1,
    pdfSeparateFragments: false,

    // Plugins
    plugins: [RevealHighlight, RevealNotes, RevealMarkdown, RevealZoom, RevealSearch]
  });
</script>
```

---

## 4. Built-in Themes

### Theme List

| Theme Name | CSS Filename | Visual Character |
|---|---|---|
| `black` | `black.css` | Dark background, white text, blue links |
| `white` | `white.css` | White background, black text, blue links |
| `league` | `league.css` | Dark gray background, off-white text, yellow headings |
| `beige` | `beige.css` | Warm beige background, dark brown text |
| `night` | `night.css` | Black background, white text, orange headings |
| `serif` | `serif.css` | Light background, serif fonts, formal appearance |
| `simple` | `simple.css` | White background, minimal styling, sans-serif |
| `solarized` | `solarized.css` | Solarized light color scheme |
| `moon` | `moon.css` | Dark blue-gray background, silver text |
| `dracula` | `dracula.css` | Dark purple background, Dracula color palette |
| `sky` | `sky.css` | Blue sky gradient background, dark text |
| `blood` | `blood.css` | Dark background, red accent headings |
| `black-contrast` | `black-contrast.css` | High-contrast black (v5+ only) |
| `white-contrast` | `white-contrast.css` | High-contrast white (v5+ only) |

### Theme Usage

```html
<!-- In <head>, after reveal.css -->
<link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/dist/theme/moon.css" />
```

### CSS Custom Properties (--r-* Variables)

All reveal.js themes expose these CSS custom properties. Override them in a `<style>` block after the theme `<link>` to customize without a build step.

| Variable | Description |
|---|---|
| `--r-background-color` | Slide background color |
| `--r-main-font` | Body/content font family |
| `--r-main-font-size` | Base font size (default: `42px`) |
| `--r-main-color` | Body text color |
| `--r-heading-font` | Heading font family |
| `--r-heading-color` | Heading text color |
| `--r-heading-font-weight` | Heading font weight (default: `600`) |
| `--r-heading-line-height` | Heading line height (default: `1.2`) |
| `--r-heading-letter-spacing` | Heading letter spacing (default: `-0.05em`) |
| `--r-heading-text-transform` | Heading text transform (default: `uppercase`) |
| `--r-heading-text-shadow` | Heading text shadow |
| `--r-heading1-size` | h1 font size (default: `2.5em`) |
| `--r-heading2-size` | h2 font size (default: `1.6em`) |
| `--r-heading3-size` | h3 font size (default: `1.3em`) |
| `--r-heading4-size` | h4 font size (default: `1.0em`) |
| `--r-heading1-text-shadow` | h1-specific text shadow |
| `--r-heading-margin` | Margin below headings (default: `0 0 20px 0`) |
| `--r-block-margin` | Margin for block elements (default: `20px`) |
| `--r-link-color` | Hyperlink color |
| `--r-link-color-hover` | Hyperlink hover color |
| `--r-link-color-dark` | Darker variant of link color |
| `--r-selection-color` | Text selection foreground color |
| `--r-selection-background-color` | Text selection background color |
| `--r-code-font` | Monospace font for `<code>` elements |

### Custom Theme via Inline Style (No SASS Required)

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/dist/reset.css" />
    <link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/dist/reveal.css" />
    <!-- Start with a base theme -->
    <link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/dist/theme/black.css" />
    <!-- Override theme variables -->
    <style>
      :root {
        --r-background-color: #1a1a2e;
        --r-main-font: 'Segoe UI', Helvetica, sans-serif;
        --r-main-font-size: 38px;
        --r-main-color: #e0e0e0;
        --r-heading-font: 'Segoe UI', Helvetica, sans-serif;
        --r-heading-color: #00d4ff;
        --r-heading-font-weight: 700;
        --r-heading-text-transform: none;
        --r-heading-letter-spacing: normal;
        --r-heading1-size: 2.2em;
        --r-heading2-size: 1.5em;
        --r-heading3-size: 1.2em;
        --r-heading4-size: 1.0em;
        --r-link-color: #00d4ff;
        --r-link-color-hover: #66e0ff;
        --r-selection-background-color: #00d4ff;
        --r-selection-color: #1a1a2e;
        --r-code-font: 'Fira Code', 'Courier New', monospace;
      }
    </style>
  </head>
  <body>
    <div class="reveal">
      <div class="slides">
        <section>
          <h1>Custom Theme</h1>
          <p>Styled via CSS custom properties</p>
        </section>
      </div>
    </div>
    <script src="https://unpkg.com/reveal.js@4.6.1/dist/reveal.js"></script>
    <script>Reveal.initialize();</script>
  </body>
</html>
```

---

## 5. Transitions

### Transition Types

| Name | Effect |
|---|---|
| `none` | Instant cut with no animation |
| `fade` | Cross-fade between slides |
| `slide` | Slides horizontally (default) |
| `convex` | Convex 3D rotation |
| `concave` | Concave 3D rotation |
| `zoom` | Zoom in/out |

### Transition Speed

| Name | Effect |
|---|---|
| `default` | Standard speed (~600ms) |
| `fast` | Faster (~300ms) |
| `slow` | Slower (~1200ms) |

### Global Transition (via Config)

```javascript
Reveal.initialize({
  transition: 'slide',
  transitionSpeed: 'default',
  backgroundTransition: 'fade'
});
```

### Per-Slide Transition Override

```html
<!-- Override transition type for this slide -->
<section data-transition="zoom">
  <h2>This slide zooms in</h2>
</section>

<!-- Override transition speed for this slide -->
<section data-transition-speed="fast">
  <h2>Fast transition</h2>
</section>

<!-- Override both type and speed -->
<section data-transition="convex" data-transition-speed="slow">
  <h2>Slow convex transition</h2>
</section>
```

### Split In/Out Transitions

Specify different transitions for entering (in) and leaving (out) a slide.

```html
<!-- Convex when entering, fade when leaving -->
<section data-transition="convex-in fade-out">
  <h2>Convex in, fade out</h2>
</section>

<!-- Slide when entering, zoom when leaving -->
<section data-transition="slide-in zoom-out">
  <h2>Slide in, zoom out</h2>
</section>

<!-- Fade in, no transition out -->
<section data-transition="fade-in none-out">
  <h2>Fade in, cut out</h2>
</section>
```

Valid suffixes: `-in`, `-out`. Combine any transition name with either suffix.

### Per-Slide Background Transition Override

```html
<section data-background-color="#8b0000" data-background-transition="slide">
  <h2>Background slides in</h2>
</section>
```

---

## 6. Fragments

Fragments reveal content step by step within a single slide. Add the `fragment` class plus an optional effect class to any element.

### All Fragment Effect Classes

| Class | Effect Description |
|---|---|
| `fragment` | Default fade-in |
| `fade-up` | Fade in while moving up |
| `fade-down` | Fade in while moving down |
| `fade-left` | Fade in while moving left |
| `fade-right` | Fade in while moving right |
| `fade-out` | Fade out on reveal |
| `semi-fade-out` | Fade to 50% opacity |
| `fade-in-then-out` | Fade in, then fade out when next fragment appears |
| `current-visible` | Visible only while it is the current fragment |
| `fade-in-then-semi-out` | Fade in, then fade to 50% opacity |
| `grow` | Grow in size |
| `shrink` | Shrink in size |
| `strike` | Strikethrough text |
| `highlight-red` | Highlight text in red |
| `highlight-green` | Highlight text in green |
| `highlight-blue` | Highlight text in blue |
| `highlight-current-red` | Highlight red only while current |
| `highlight-current-green` | Highlight green only while current |
| `highlight-current-blue` | Highlight blue only while current |

### Basic Fragment Usage

```html
<section>
  <h2>Shopping List</h2>
  <ul>
    <li class="fragment">Milk</li>
    <li class="fragment fade-up">Eggs</li>
    <li class="fragment highlight-red">Butter</li>
    <li class="fragment fade-out">Cheese (optional)</li>
  </ul>
</section>
```

### Fragment Ordering with data-fragment-index

Fragments appear in ascending `data-fragment-index` order. Elements with the same index appear simultaneously.

```html
<section>
  <!-- These appear simultaneously (both index 1) -->
  <p class="fragment" data-fragment-index="1">First group - item A</p>
  <p class="fragment" data-fragment-index="1">First group - item B</p>
  <!-- This appears after (index 2) -->
  <p class="fragment" data-fragment-index="2">Second group</p>
  <!-- This appears first (index 0) -->
  <p class="fragment" data-fragment-index="0">Actually appears first</p>
</section>
```

### Nested Fragments

Wrap elements in a span to create nested or compound fragment effects.

```html
<section>
  <p>
    <span class="fragment fade-in">
      <span class="fragment fade-out">
        Fades in then fades out when next fragment is triggered
      </span>
    </span>
  </p>
</section>
```

### Custom Fragment CSS

Create a custom fragment effect named `flip` as an example.

```html
<style>
  /* Initial (hidden) state */
  .fragment.flip {
    transform: rotateY(90deg);
    opacity: 0;
    transition: transform 0.4s ease, opacity 0.4s ease;
  }
  /* Revealed (visible) state */
  .fragment.flip.visible {
    transform: rotateY(0deg);
    opacity: 1;
  }
</style>

<section>
  <h2 class="fragment flip">Custom flip effect</h2>
</section>
```

---

## 7. Backgrounds

Background attributes are placed on `<section>` elements.

### Color Background

```html
<!-- Hex color -->
<section data-background-color="#3d6b84">
  <h2>Hex color background</h2>
</section>

<!-- RGBA -->
<section data-background-color="rgba(255, 100, 50, 0.8)">
  <h2>RGBA color background</h2>
</section>

<!-- HSL -->
<section data-background-color="hsl(210, 50%, 30%)">
  <h2>HSL color background</h2>
</section>

<!-- CSS keyword -->
<section data-background-color="coral">
  <h2>Keyword color background</h2>
</section>
```

### Gradient Background

```html
<!-- Linear gradient -->
<section data-background-gradient="linear-gradient(to bottom right, #283b95, #17b2c3)">
  <h2>Linear gradient</h2>
</section>

<!-- Radial gradient -->
<section data-background-gradient="radial-gradient(circle at center, #4a00e0, #8e2de2)">
  <h2>Radial gradient</h2>
</section>

<!-- Conic gradient -->
<section data-background-gradient="conic-gradient(from 0deg, #ff6b6b, #ffd93d, #6bcb77, #4d96ff, #ff6b6b)">
  <h2>Conic gradient</h2>
</section>
```

### Image Background

| Attribute | Values | Description |
|---|---|---|
| `data-background-image` | URL string | Path or URL to the image |
| `data-background-size` | `cover` (default), `contain`, CSS size | CSS `background-size` |
| `data-background-position` | `center` (default), CSS position | CSS `background-position` |
| `data-background-repeat` | `no-repeat` (default), `repeat`, `repeat-x`, `repeat-y` | CSS `background-repeat` |
| `data-background-opacity` | `0` to `1` | Image opacity (content remains fully opaque) |

```html
<!-- Full-cover image -->
<section data-background-image="https://picsum.photos/1920/1080">
  <h2>Cover image background</h2>
</section>

<!-- Contained image with custom position -->
<section
  data-background-image="logo.png"
  data-background-size="contain"
  data-background-position="top right"
  data-background-repeat="no-repeat"
  data-background-color="#111"
>
  <h2>Contained image</h2>
</section>

<!-- Dimmed image background -->
<section
  data-background-image="https://picsum.photos/1920/1080"
  data-background-opacity="0.3"
>
  <h2>Readable text over dimmed image</h2>
</section>
```

### Video Background

| Attribute | Values | Description |
|---|---|---|
| `data-background-video` | URL or comma-separated URLs | Video source(s) |
| `data-background-video-loop` | (boolean attribute) | Loop the video |
| `data-background-video-muted` | (boolean attribute) | Mute the video |
| `data-background-size` | `cover` (default), `contain` | CSS `object-fit` equivalent |
| `data-background-opacity` | `0` to `1` | Video opacity |

```html
<!-- Looping muted background video -->
<section
  data-background-video="video.mp4,video.webm"
  data-background-video-loop
  data-background-video-muted
>
  <h2>Video background</h2>
</section>

<!-- Video with reduced opacity -->
<section
  data-background-video="intro.mp4"
  data-background-video-muted
  data-background-opacity="0.4"
>
  <h2>Dimmed video background</h2>
</section>
```

### Iframe Background

| Attribute | Values | Description |
|---|---|---|
| `data-background-iframe` | URL string | URL to load in background iframe |
| `data-background-interactive` | (boolean attribute) | Allow interaction with the iframe |
| `data-preload` | (boolean attribute) | Pre-load the iframe before the slide is reached |

```html
<!-- Non-interactive iframe background -->
<section data-background-iframe="https://example.com">
  <div style="background:rgba(0,0,0,0.7); padding:20px; border-radius:8px;">
    <h2>Website as background</h2>
  </div>
</section>

<!-- Interactive iframe (user can click/scroll within it) -->
<section
  data-background-iframe="https://www.openstreetmap.org/export/embed.html?bbox=-0.1,51.4,0.1,51.6"
  data-background-interactive
>
  <h2 style="color:white; text-shadow:1px 1px 3px #000;">Interactive Map</h2>
</section>
```

---

## 8. Layout Utilities

reveal.js provides CSS utility classes for common layout patterns. Apply them directly to elements inside `<section>`.

### r-stretch

Stretches one element to fill the remaining vertical space on a slide after other content has been rendered. Only one element per slide can use `r-stretch`.

```html
<section>
  <h2>Title</h2>
  <!-- This image fills all remaining height -->
  <img class="r-stretch" src="diagram.png" alt="Diagram" />
  <p>Caption below</p>
</section>
```

### r-fit-text

Automatically scales text to fill the full width of the slide. Useful for impactful single-line headings.

```html
<section>
  <h2 class="r-fit-text">Auto-Fit Heading</h2>
  <h2 class="r-fit-text">Another Line That Scales</h2>
</section>
```

### r-stack

Layers child elements on top of each other (absolute positioning). Commonly used with fragments to reveal elements in place.

```html
<section>
  <div class="r-stack">
    <img class="fragment fade-out" src="step1.png" alt="Step 1" />
    <img class="fragment current-visible" src="step2.png" alt="Step 2" />
    <img class="fragment" src="step3.png" alt="Step 3" />
  </div>
</section>
```

### r-hstack

Horizontal flexbox row with centered alignment. Children are placed side by side.

```html
<section>
  <div class="r-hstack">
    <div style="margin:0 20px;">
      <h3>Column A</h3>
      <p>Content A</p>
    </div>
    <div style="margin:0 20px;">
      <h3>Column B</h3>
      <p>Content B</p>
    </div>
    <div style="margin:0 20px;">
      <h3>Column C</h3>
      <p>Content C</p>
    </div>
  </div>
</section>
```

### r-vstack

Vertical flexbox column with centered alignment. Children are stacked top to bottom.

```html
<section>
  <div class="r-vstack">
    <h3>Top</h3>
    <p>Middle content</p>
    <small>Bottom note</small>
  </div>
</section>
```

### r-frame

Applies a decorative border and padding around an element to visually frame it.

```html
<section>
  <img class="r-frame" src="screenshot.png" alt="Framed screenshot" />
</section>

<section>
  <blockquote class="r-frame">
    "A framed quote stands out from surrounding content."
  </blockquote>
</section>
```

---

## 9. Speaker Notes

### aside.notes Element

Place `<aside class="notes">` anywhere inside a `<section>` to add speaker notes. The content is not shown in the presentation view.

```html
<section>
  <h2>Slide Title</h2>
  <p>Visible content</p>
  <aside class="notes">
    These are speaker notes. Only visible in the speaker view.
    You can include <strong>HTML</strong> here.
    - Bullet point one
    - Bullet point two
  </aside>
</section>
```

### data-notes Attribute

Alternatively, use the `data-notes` attribute directly on the section.

```html
<section data-notes="Speak slowly here. Emphasize the third point.">
  <h2>Quick Notes</h2>
</section>
```

### Notes in Markdown (Note: keyword)

When using the Markdown plugin, use `Note:` as a separator. Everything after it becomes speaker notes.

```html
<section data-markdown>
  <textarea data-template>
## Slide Title

Content of the slide.

Note:
These are speaker notes visible only in speaker view.
Anything after "Note:" is hidden from the audience.
  </textarea>
</section>
```

### Configuration Options for Notes

```javascript
Reveal.initialize({
  // Show notes inline in presentation (not recommended for audiences)
  showNotes: false,

  // Default time per slide in seconds (for timer in speaker view)
  defaultTiming: 120
});
```

### Per-Slide Timing

```html
<!-- This slide should take 60 seconds -->
<section data-timing="60">
  <h2>Short Slide</h2>
</section>

<!-- This slide should take 5 minutes (300 seconds) -->
<section data-timing="300">
  <h2>Long Demo Slide</h2>
  <aside class="notes">Walk through the live demo here.</aside>
</section>
```

### Opening Speaker View

Press `S` in the browser to open the speaker notes window. Requires the Notes plugin to be loaded.

```html
<script src="https://unpkg.com/reveal.js@4.6.1/plugin/notes/notes.js"></script>
<script>
  Reveal.initialize({
    plugins: [RevealNotes]
  });
</script>
```

---

## 10. Auto-Animate

Auto-animate automatically animates matching elements between two adjacent slides. Add `data-auto-animate` to both sections.

### Basic Usage

```html
<!-- Slide 1 -->
<section data-auto-animate>
  <h2>Title Here</h2>
</section>

<!-- Slide 2: h2 animates to its new position/size -->
<section data-auto-animate>
  <h2>Title Here</h2>
  <p>New paragraph appears</p>
</section>
```

### Element Matching Rules

Auto-animate matches elements using these strategies (in priority order):

1. **`data-id` attribute** — explicit match regardless of content
2. **Text content** — text nodes with identical content are matched
3. **Media src** — `<img>`, `<video>`, `<iframe>` matched by `src` attribute
4. **Element type** — same tag type at the same position

```html
<!-- Slide 1 -->
<section data-auto-animate>
  <h2>Header</h2>
  <div data-id="box" style="background:#3d6b84; width:100px; height:100px;"></div>
</section>

<!-- Slide 2: the box animates to its new size and position -->
<section data-auto-animate>
  <h2>Header</h2>
  <div data-id="box" style="background:#3d6b84; width:300px; height:100px;"></div>
</section>
```

### Per-Slide Auto-Animate Settings

```html
<section data-auto-animate data-auto-animate-easing="cubic-bezier(0.770, 0.000, 0.175, 1.000)">
  <h2>Custom Easing</h2>
</section>

<section data-auto-animate data-auto-animate-duration="2.0">
  <h2>Slow 2-Second Animation</h2>
</section>

<!-- Disable animation for unmatched elements on this slide -->
<section data-auto-animate data-auto-animate-unmatched="false">
  <h2>No fade for new elements</h2>
</section>
```

### Per-Element Animation Delay

```html
<section data-auto-animate>
  <h2>Results</h2>
  <ul>
    <li data-auto-animate-delay="0">Item one</li>
    <li data-auto-animate-delay="0.1">Item two</li>
    <li data-auto-animate-delay="0.2">Item three</li>
  </ul>
</section>
```

### Auto-Animate Groups

Use `data-auto-animate-id` to match slides across non-adjacent positions. Use `data-auto-animate-restart` to break a group.

```html
<section data-auto-animate data-auto-animate-id="intro">
  <h2>Group A - Step 1</h2>
</section>

<section data-auto-animate data-auto-animate-id="intro">
  <h2>Group A - Step 2</h2>
</section>

<!-- data-auto-animate-restart starts a new chain even if data-auto-animate-id matches -->
<section data-auto-animate data-auto-animate-id="intro" data-auto-animate-restart>
  <h2>Group A Restarted</h2>
</section>
```

### Code Block Auto-Animate

Assign the same `data-id` to `<code>` elements across two slides to animate code changes.

```html
<!-- Slide 1 -->
<section data-auto-animate>
  <pre><code data-id="code-block" class="javascript">
function greet() {
  console.log("Hello");
}
  </code></pre>
</section>

<!-- Slide 2: code morphs from previous state -->
<section data-auto-animate>
  <pre><code data-id="code-block" class="javascript">
function greet(name) {
  const message = `Hello, ${name}!`;
  console.log(message);
}
  </code></pre>
</section>
```

---

## 11. Code Highlighting

Requires the RevealHighlight plugin. Uses highlight.js under the hood.

### Plugin Setup

```html
<link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/plugin/highlight/monokai.css" />
<script src="https://unpkg.com/reveal.js@4.6.1/plugin/highlight/highlight.js"></script>
<script>
  Reveal.initialize({
    plugins: [RevealHighlight]
  });
</script>
```

### Basic Code Block

```html
<section>
  <pre><code class="language-javascript">
const greet = (name) => `Hello, ${name}!`;
console.log(greet("World"));
  </code></pre>
</section>
```

### Supported Language Classes

Use `class="language-NAME"` or `class="NAME"` on the `<code>` element.

Common values: `javascript`, `typescript`, `python`, `java`, `go`, `rust`, `c`, `cpp`, `csharp`, `html`, `css`, `scss`, `json`, `yaml`, `bash`, `shell`, `sql`, `markdown`, `xml`, `plaintext`

### data-line-numbers

```html
<!-- Enable line numbers (no specific highlighting) -->
<pre><code class="language-python" data-line-numbers>
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)
</code></pre>

<!-- Highlight line 2 -->
<pre><code class="language-python" data-line-numbers="2">
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)
</code></pre>

<!-- Highlight a range: lines 1 through 3 -->
<pre><code class="language-python" data-line-numbers="1-3">
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)
</code></pre>

<!-- Highlight specific non-contiguous lines -->
<pre><code class="language-python" data-line-numbers="1,4">
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)
</code></pre>
```

### Step-by-Step Line Highlighting (pipe separator)

Each pipe `|` character creates a new fragment step.

```html
<pre><code class="language-javascript" data-line-numbers="1-2|3-5|6-8|9">
// Step 1: imports shown (lines 1-2)
import React, { useState } from 'react';
// Step 2: component definition (lines 3-5)
function Counter() {
  const [count, setCount] = useState(0);
// Step 3: JSX (lines 6-8)
  return (
    &lt;button onClick={() =&gt; setCount(count + 1)}&gt;
// Step 4: close (line 9)
    &lt;/button&gt;
  );
}
</code></pre>
```

### Additional Code Attributes

| Attribute | Effect |
|---|---|
| `data-trim` | Strips leading/trailing whitespace from the code block |
| `data-noescape` | Prevents HTML entity escaping (use when code contains `<` or `>`) |
| `data-ln-start-from="N"` | Start line numbering from N instead of 1 |

```html
<pre><code class="language-html" data-trim data-noescape data-line-numbers>
<div class="container">
  <p>HTML without escaping</p>
</div>
</code></pre>

<!-- Start line numbers from 10 (e.g., showing an excerpt) -->
<pre><code class="language-python" data-line-numbers data-ln-start-from="10" data-trim>
    result = process(data)
    return result
</code></pre>
```

---

## 12. Markdown Support

Requires the RevealMarkdown plugin.

### Plugin Setup

```html
<script src="https://unpkg.com/reveal.js@4.6.1/plugin/markdown/markdown.js"></script>
<script>
  Reveal.initialize({
    plugins: [RevealMarkdown]
  });
</script>
```

### Inline Markdown

Use `data-markdown` on the section and `<textarea data-template>` to hold the content.

```html
<section data-markdown>
  <textarea data-template>
## Slide Title

- Bullet one
- Bullet two
- Bullet three

Note:
Speaker notes go here.
  </textarea>
</section>
```

### Slide Separator in Inline Markdown

Use `---` (three dashes) to create a new horizontal slide. Use `--` (two dashes) for vertical slides.

```html
<section data-markdown>
  <textarea data-template>
# Slide 1

---

# Slide 2

--

# Slide 2b (Vertical)

---

# Slide 3
  </textarea>
</section>
```

### External Markdown File

```html
<section
  data-markdown="slides.md"
  data-separator="^\n---\n"
  data-separator-vertical="^\n--\n"
  data-separator-notes="^Note:"
  data-charset="utf-8"
>
</section>
```

`slides.md` example:

```markdown
# First Slide

Content here.

---

# Second Slide

More content.

Note:
Speaker notes for slide 2.
```

### Element Attributes in Markdown

Append `<!-- .element: -->` comments after an element to add HTML attributes to it.

```markdown
## Title

- Item one
- Item two
<!-- .element: class="fragment" -->
- Item three
<!-- .element: class="fragment fade-up" data-fragment-index="1" -->
```

### Slide Attributes in Markdown

Use `<!-- .slide: -->` to add attributes to the containing `<section>` element.

```markdown
## Dark Background Slide

<!-- .slide: data-background-color="#2c3e50" -->

Content on a dark slide.

---

## Animated Slide

<!-- .slide: data-auto-animate -->

Content here.
```

---

## 13. Plugins

### RevealHighlight

Syntax highlighting using highlight.js.

- CDN JS: `https://unpkg.com/reveal.js@4.6.1/plugin/highlight/highlight.js`
- CDN CSS (pick one): `https://unpkg.com/reveal.js@4.6.1/plugin/highlight/monokai.css` or `zenburn.css`
- Plugin array name: `RevealHighlight`

```html
<link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/plugin/highlight/monokai.css" />
<script src="https://unpkg.com/reveal.js@4.6.1/plugin/highlight/highlight.js"></script>
<script>
  Reveal.initialize({
    highlight: {
      highlightOnLoad: true  // Highlight all code blocks on initialization
    },
    plugins: [RevealHighlight]
  });
</script>
```

### RevealMarkdown

Markdown slide authoring.

- CDN JS: `https://unpkg.com/reveal.js@4.6.1/plugin/markdown/markdown.js`
- Plugin array name: `RevealMarkdown`

```html
<script src="https://unpkg.com/reveal.js@4.6.1/plugin/markdown/markdown.js"></script>
<script>
  Reveal.initialize({
    markdown: {
      smartypants: true  // Convert ASCII quotes and dashes to typographic equivalents
    },
    plugins: [RevealMarkdown]
  });
</script>
```

### RevealNotes

Speaker notes window (press `S` to open).

- CDN JS: `https://unpkg.com/reveal.js@4.6.1/plugin/notes/notes.js`
- Plugin array name: `RevealNotes`

```html
<script src="https://unpkg.com/reveal.js@4.6.1/plugin/notes/notes.js"></script>
<script>
  Reveal.initialize({
    plugins: [RevealNotes]
  });
  // Press S to open speaker view in a new window
</script>
```

### RevealSearch

Full-text search through slides (press `Ctrl+Shift+F`).

- CDN JS: `https://unpkg.com/reveal.js@4.6.1/plugin/search/search.js`
- Plugin array name: `RevealSearch`

```html
<script src="https://unpkg.com/reveal.js@4.6.1/plugin/search/search.js"></script>
<script>
  Reveal.initialize({
    plugins: [RevealSearch]
  });
  // Ctrl+Shift+F opens search overlay
</script>
```

### RevealZoom

Alt+Click to zoom into any slide element.

- CDN JS: `https://unpkg.com/reveal.js@4.6.1/plugin/zoom/zoom.js`
- Plugin array name: `RevealZoom`

```html
<script src="https://unpkg.com/reveal.js@4.6.1/plugin/zoom/zoom.js"></script>
<script>
  Reveal.initialize({
    plugins: [RevealZoom]
  });
  // Alt+Click (Option+Click on Mac) to zoom into elements
</script>
```

### RevealMath

Render mathematical notation. Supports KaTeX (recommended), MathJax2, and MathJax3.

- CDN JS: `https://unpkg.com/reveal.js@4.6.1/plugin/math/math.js`
- Plugin array name: `RevealMath.KaTeX`, `RevealMath.MathJax2`, or `RevealMath.MathJax3`

#### KaTeX (Recommended — Fast, No External CDN Needed)

```html
<script src="https://unpkg.com/reveal.js@4.6.1/plugin/math/math.js"></script>
<script>
  Reveal.initialize({
    math: {
      mathjax: 'https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js',
      config: 'TeX-AMS_HTML-full',
      // KaTeX options
      katex: {
        version: 'latest',
        delimiters: [
          { left: '$$', right: '$$', display: true },
          { left: '$', right: '$', display: false },
          { left: '\\(', right: '\\)', display: false },
          { left: '\\[', right: '\\]', display: true }
        ],
        ignoredTags: ['script', 'noscript', 'style', 'textarea', 'pre']
      }
    },
    plugins: [RevealMath.KaTeX]
  });
</script>
```

#### MathJax3

```html
<script src="https://unpkg.com/reveal.js@4.6.1/plugin/math/math.js"></script>
<script>
  Reveal.initialize({
    math: {
      mathjax: 'https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js',
      tex: {
        inlineMath: [['$', '$'], ['\\(', '\\)']],
        displayMath: [['$$', '$$'], ['\\[', '\\]']]
      }
    },
    plugins: [RevealMath.MathJax3]
  });
</script>
```

#### Math Syntax Examples

```html
<section>
  <h2>Inline Math</h2>
  <!-- KaTeX/MathJax inline: wrap in $ ... $ -->
  <p>The area of a circle is $A = \pi r^2$</p>

  <h2>Display Math</h2>
  <!-- Block/display: wrap in $$ ... $$ -->
  <p>$$\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}$$</p>

  <h2>Fractions and Summations</h2>
  <p>$$\sum_{n=1}^{\infty} \frac{1}{n^2} = \frac{\pi^2}{6}$$</p>

  <h2>Matrix</h2>
  <p>$$\begin{pmatrix} a & b \\ c & d \end{pmatrix}$$</p>
</section>
```

### Full Plugin Setup Example

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/dist/reset.css" />
    <link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/dist/reveal.css" />
    <link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/dist/theme/black.css" />
    <link rel="stylesheet" href="https://unpkg.com/reveal.js@4.6.1/plugin/highlight/monokai.css" />
  </head>
  <body>
    <div class="reveal">
      <div class="slides">
        <section>Slide 1</section>
      </div>
    </div>
    <script src="https://unpkg.com/reveal.js@4.6.1/dist/reveal.js"></script>
    <script src="https://unpkg.com/reveal.js@4.6.1/plugin/highlight/highlight.js"></script>
    <script src="https://unpkg.com/reveal.js@4.6.1/plugin/markdown/markdown.js"></script>
    <script src="https://unpkg.com/reveal.js@4.6.1/plugin/notes/notes.js"></script>
    <script src="https://unpkg.com/reveal.js@4.6.1/plugin/search/search.js"></script>
    <script src="https://unpkg.com/reveal.js@4.6.1/plugin/zoom/zoom.js"></script>
    <script src="https://unpkg.com/reveal.js@4.6.1/plugin/math/math.js"></script>
    <script>
      Reveal.initialize({
        plugins: [RevealHighlight, RevealMarkdown, RevealNotes, RevealSearch, RevealZoom, RevealMath.KaTeX]
      });
    </script>
  </body>
</html>
```

---

## 14. PDF Export

### Browser-Based Export

1. Append `?print-pdf` to the presentation URL:
   ```
   http://localhost:8000/index.html?print-pdf
   ```

2. Open the browser print dialog (`Ctrl+P` / `Cmd+P`).

3. Configure print settings:
   - **Layout:** Landscape
   - **Margins:** None
   - **Background graphics:** Enabled (checked)
   - **Scale:** 100%

4. Save as PDF.

### Recommended Configuration for Clean PDF Output

```javascript
Reveal.initialize({
  // Ensure each slide fits on exactly one page
  pdfMaxPagesPerSlide: 1,
  // All fragment states on a single page (do not create separate pages per fragment)
  pdfSeparateFragments: false
});
```

### decktape CLI (Automated PDF Generation)

decktape produces higher-quality PDFs than browser printing and supports all slide features.

```bash
# Install and run in one command (no global install needed)
npx decktape reveal http://localhost:8000/index.html output.pdf

# Specify slide size
npx decktape reveal --size 1920x1080 http://localhost:8000/index.html output.pdf

# Set pause between slides (milliseconds) for animations to complete
npx decktape reveal --pause 1000 http://localhost:8000/index.html output.pdf

# Export specific slides (1-indexed)
npx decktape reveal --slides 1-10 http://localhost:8000/index.html output.pdf
```

### Notes on PDF Export

- The `?print-pdf` mode applies a special CSS layout that stacks all slides vertically.
- Vertical (nested) slides are linearized in sequence.
- Video backgrounds are not rendered in PDFs; use a poster image as fallback.
- Iframe backgrounds are not rendered in PDFs.
- Fragment animations are collapsed to their final state (all visible) unless `pdfSeparateFragments: true`.

---

## 15. Quick Reference Cheat Sheet

### Table 1: Section (Slide) Attributes

All `data-*` attributes valid on `<section>` elements.

| Attribute | Example Value | Purpose |
|---|---|---|
| `id` | `"my-slide"` | Named anchor for URL navigation (`#/my-slide`) |
| `data-state` | `"custom-class"` | Adds class to `.reveal` when slide is active |
| `data-visibility` | `"hidden"` / `"uncounted"` | Hide slide from navigation |
| `data-transition` | `"zoom"` / `"fade-in slide-out"` | Override transition for this slide |
| `data-transition-speed` | `"fast"` / `"slow"` / `"default"` | Override transition speed |
| `data-background-transition` | `"slide"` | Override background transition |
| `data-background-color` | `"#ff0000"` / `"rgba(…)"` / `"hsl(…)"` | Solid color background |
| `data-background-gradient` | `"linear-gradient(…)"` | CSS gradient background |
| `data-background-image` | `"image.jpg"` | Image background URL |
| `data-background-size` | `"cover"` / `"contain"` | Image/video background sizing |
| `data-background-position` | `"center"` / `"top left"` | Image background position |
| `data-background-repeat` | `"no-repeat"` / `"repeat"` | Image background repeat |
| `data-background-opacity` | `"0.5"` | Opacity of background image/video (0–1) |
| `data-background-video` | `"video.mp4,video.webm"` | Video background source(s) |
| `data-background-video-loop` | (boolean, no value) | Loop background video |
| `data-background-video-muted` | (boolean, no value) | Mute background video |
| `data-background-iframe` | `"https://example.com"` | Iframe background URL |
| `data-background-interactive` | (boolean, no value) | Enable interaction with iframe background |
| `data-preload` | (boolean, no value) | Pre-load iframe before slide is reached |
| `data-auto-animate` | (boolean, no value) | Enable auto-animate with adjacent slide |
| `data-auto-animate-id` | `"group-name"` | Group slides for auto-animate matching |
| `data-auto-animate-restart` | (boolean, no value) | Restart auto-animate group chain |
| `data-auto-animate-easing` | `"ease-in-out"` | CSS easing for auto-animate on this slide |
| `data-auto-animate-duration` | `"0.8"` | Duration in seconds for auto-animate |
| `data-auto-animate-unmatched` | `"false"` | Disable fade for unmatched elements |
| `data-markdown` | `"slides.md"` or (no value) | Enable Markdown for this section |
| `data-separator` | `"^\n---\n"` | Regex to split horizontal slides in Markdown |
| `data-separator-vertical` | `"^\n--\n"` | Regex to split vertical slides in Markdown |
| `data-separator-notes` | `"^Note:"` | Regex to identify speaker notes in Markdown |
| `data-charset` | `"utf-8"` | Character set for external Markdown file |
| `data-timing` | `"120"` | Expected time in seconds for speaker timer |
| `data-notes` | `"Speak slowly here"` | Inline speaker notes string |

---

### Table 2: Fragment Effect Classes

Apply to any child element inside `<section>` along with the base `fragment` class.

| Class | Effect |
|---|---|
| `fragment` | Fade in (default effect) |
| `fragment fade-up` | Fade in while moving upward |
| `fragment fade-down` | Fade in while moving downward |
| `fragment fade-left` | Fade in while moving left |
| `fragment fade-right` | Fade in while moving right |
| `fragment fade-out` | Fade out when triggered |
| `fragment semi-fade-out` | Fade to 50% opacity |
| `fragment fade-in-then-out` | Fade in, then fade out on next step |
| `fragment current-visible` | Visible only while it is the current step |
| `fragment fade-in-then-semi-out` | Fade in, then fade to 50% on next step |
| `fragment grow` | Scale up when triggered |
| `fragment shrink` | Scale down when triggered |
| `fragment strike` | Apply strikethrough text decoration |
| `fragment highlight-red` | Turn text red permanently |
| `fragment highlight-green` | Turn text green permanently |
| `fragment highlight-blue` | Turn text blue permanently |
| `fragment highlight-current-red` | Red only while current step |
| `fragment highlight-current-green` | Green only while current step |
| `fragment highlight-current-blue` | Blue only while current step |

---

### Table 3: Element-Level Attributes

All `data-*` attributes valid on child elements inside `<section>`.

| Attribute | Example Value | Purpose |
|---|---|---|
| `data-fragment-index` | `"2"` | Order in which fragment appears; same index = simultaneous |
| `data-id` | `"unique-id"` | Explicit match key for auto-animate across slides |
| `data-auto-animate-delay` | `"0.2"` | Delay in seconds before this element animates |
| `data-auto-animate-duration` | `"0.5"` | Per-element animation duration override |
| `data-auto-animate-easing` | `"ease-in"` | Per-element CSS easing override |
| `data-line-numbers` | `"1-3\|5\|7-9"` | Enable/highlight line numbers in `<code>` blocks |
| `data-trim` | (boolean, no value) | Strip whitespace from `<code>` block |
| `data-noescape` | (boolean, no value) | Disable HTML escaping in `<code>` block |
| `data-ln-start-from` | `"10"` | Start line number counter at N in `<code>` blocks |
| `data-src` | `"slides.md"` | Source URL for `<textarea data-template>` in Markdown |
| `data-markdown` | (no value) | Alias for inline Markdown on a `<textarea>` |
| `data-preview-link` | `"true"` / `"false"` | Override `previewLinks` for a specific `<a>` element |

---

*End of reveal.js API Reference (v4.6.1)*
