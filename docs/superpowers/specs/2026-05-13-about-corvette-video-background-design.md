# Design Spec: About Section — Corvette Video Background

**Date:** 2026-05-13
**Status:** Approved
**Scope:** `index.html` — About section only

---

## Summary

Replace the static two-column About section (light background + right-column image) with a full-viewport cinematic dark section. The Corvette ShowRoom Video plays silently as a full-bleed atmospheric background. All existing copy is preserved and reflows into a single centered editorial column.

---

## Layout & Structure

- `#about` height: `min-height: 100vh`
- Remove the `--light-bg` background color — video provides the environment
- `.about-inner` changes from a 2-column grid (`1fr 1fr`) to a single centered column (`max-width: 720px; margin: 0 auto`)
- Remove the `.about-image` div and its child `<img>` entirely
- Top gold rule border (`#about::before`) stays — marks the section transition against the nav above
- Existing `.reveal` scroll-trigger classes remain untouched

## Video Element

```html
<video
  class="about-video-bg"
  src="Brand Assets/Corvette ShowRoom Video.mp4"
  autoplay
  muted
  loop
  playsinline
  preload="none"
  aria-hidden="true"
></video>
```

- `position: absolute; inset: 0; width: 100%; height: 100%; object-fit: cover; z-index: 0`
- `aria-hidden="true"` — purely decorative, not announced to screen readers
- Fallback: if video fails to load, `#about` falls back to `background: #0a0a0f` (solid dark). Text remains fully readable.

## Overlay

A four-stop gradient between the video and the text content:

```css
background: linear-gradient(
  to bottom,
  rgba(10,10,15,0.78) 0%,
  rgba(10,10,15,0.40) 35%,
  rgba(10,10,15,0.40) 65%,
  rgba(10,10,15,0.78) 100%
);
```

- `position: absolute; inset: 0; z-index: 1`
- Darkens top and bottom edges, lets the center of the footage show through
- No blur, no grain — video provides its own texture

## Typography

All text flips from light-section to dark-section palette:

| Element | Value |
|---|---|
| Eyebrow ("Our Story") | `var(--gold)` |
| Heading | `#ffffff` |
| Heading `<em>` | `var(--gold)` italic |
| Gold rule | `var(--gold)`, opacity `0.45` |
| Body paragraphs | `rgba(255,255,255,0.82)` |
| Pillar labels (Speed / Luxury / Sustain) | `#ffffff` |
| Pillar sub-labels | `var(--gold)` |
| Pillar border-top | `rgba(255,255,255,0.14)` |

Text alignment: **centered** within the 720px container — matches the cinematic editorial tone.

## z-index Stack

```
z-index 0 — <video> (background)
z-index 1 — gradient overlay
z-index 2 — .about-inner (text content)
```

## What Is NOT Changed

- All existing copy text (three paragraphs + three pillars)
- Eyebrow label ("Our Story")
- Heading ("Puerto Rico's Premier Executive Carwash")
- `.reveal` scroll-trigger animations
- Top gold rule `::before` pseudo-element
- Section ID and ARIA label
- Nav anchor link (`#about`)

## Files Changed

- `index.html` — About section HTML and inline CSS only

## Assets Used

- `Brand Assets/Corvette ShowRoom Video.mp4` — already present in repo
