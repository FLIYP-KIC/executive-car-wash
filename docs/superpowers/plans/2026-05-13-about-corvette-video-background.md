# About Section — Corvette Video Background Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the About section's light two-column layout with a full-viewport cinematic dark section using the Corvette ShowRoom Video as an atmospheric background.

**Architecture:** All changes are contained in a single `index.html` file with inline CSS and HTML. No build step. The video element is positioned absolute behind a gradient overlay; text content sits above via z-index stacking.

**Tech Stack:** Plain HTML/CSS, no frameworks, no build tools. Local server via `node serve.mjs`. Screenshots via `node screenshot.mjs`.

---

## Files

| File | Change |
|------|--------|
| `index.html` | CSS: update `#about`, `.about-inner`, text color rules, add `.about-video-bg` + `.about-overlay`, remove `.about-image` block |
| `index.html` | HTML: add `<video>` + overlay div, remove `.about-image` div |

---

## Task 1: Take a before screenshot

**Files:**
- Read: `index.html` (no changes)
- Output: `temporary screenshots/before-about-video.png`

- [ ] **Step 1: Start the local server (if not already running)**

```bash
node serve.mjs &
```

Expected: `Listening on http://localhost:3000`

- [ ] **Step 2: Take the before screenshot**

```bash
node screenshot.mjs http://localhost:3000 before-about-video
```

Expected: A PNG saved to `temporary screenshots/` showing the current light two-column About section.

- [ ] **Step 3: Read the screenshot to confirm it captured the About section**

Use the Read tool on the saved PNG. Verify the light cream background and two-column layout with the static image on the right are visible.

---

## Task 2: Update `#about` CSS — section container

**Files:**
- Modify: `index.html` lines 231–236

The `#about` block must become dark, full-viewport, and overflow-hidden to contain the absolutely-positioned video.

- [ ] **Step 1: Replace the `#about` CSS block**

Find this exact block (lines 231–236):

```css
    /* ─── About (Light) ─────────────────────────────────── */
    #about {
      background: var(--light-bg);
      padding: clamp(6rem, 12vw, 10rem) 0;
      position: relative;
    }
```

Replace with:

```css
    /* ─── About (Cinematic) ─────────────────────────────── */
    #about {
      background: #0a0a0f;
      min-height: 100vh;
      padding: clamp(6rem, 12vw, 10rem) 0;
      position: relative;
      overflow: hidden;
    }
```

Changes: comment rename, `background` to dark fallback, add `min-height: 100vh`, add `overflow: hidden`. The `#about::before` gold rule line stays untouched.

- [ ] **Step 2: Verify the edit is correct**

Read lines 231–237 of `index.html`. Confirm:
- Comment says "Cinematic" not "Light"
- `background: #0a0a0f`
- `min-height: 100vh` is present
- `overflow: hidden` is present
- `#about::before` block directly follows and is unchanged

---

## Task 3: Add `.about-video-bg` and `.about-overlay` CSS

**Files:**
- Modify: `index.html` — insert after the `#about::before { ... }` block (after line 243)

- [ ] **Step 1: Insert new CSS classes after `#about::before`**

Find this exact text (line 243):

```css
    }
    .about-inner {
```

Replace with:

```css
    }
    .about-video-bg {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
      z-index: 0;
    }
    .about-overlay {
      position: absolute;
      inset: 0;
      background: linear-gradient(
        to bottom,
        rgba(10,10,15,0.78) 0%,
        rgba(10,10,15,0.40) 35%,
        rgba(10,10,15,0.40) 65%,
        rgba(10,10,15,0.78) 100%
      );
      z-index: 1;
      pointer-events: none;
    }
    .about-inner {
```

- [ ] **Step 2: Verify the insertion**

Read the modified area. Confirm `.about-video-bg` and `.about-overlay` classes are present between `#about::before { }` and `.about-inner { }`, with the correct z-index values (0 and 1 respectively).

---

## Task 4: Update `.about-inner` CSS — single centered column

**Files:**
- Modify: `index.html` — the `.about-inner` block and its media query

The inner container must drop from a 2-column grid to a single centered column, narrow to 720px, and stack above the overlay via `z-index: 2`.

- [ ] **Step 1: Replace the `.about-inner` block and its media query**

Find this exact block:

```css
    .about-inner {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 clamp(1.5rem, 6vw, 5rem);
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: clamp(3rem, 7vw, 7rem);
      align-items: center;
    }
    @media (max-width: 768px) {
      .about-inner { grid-template-columns: 1fr; }
    }
```

Replace with:

```css
    .about-inner {
      max-width: 720px;
      margin: 0 auto;
      padding: 0 clamp(1.5rem, 6vw, 5rem);
      position: relative;
      z-index: 2;
      text-align: center;
    }
```

Changes: `max-width` narrowed to 720px, grid removed, `position: relative; z-index: 2` added, `text-align: center` added, mobile media query removed (no longer needed — single column at all widths).

- [ ] **Step 2: Verify the edit**

Read the `.about-inner` block. Confirm: no `display: grid`, no `grid-template-columns`, `max-width: 720px`, `z-index: 2`, `text-align: center`.

---

## Task 5: Update text color CSS — flip from light to dark palette

**Files:**
- Modify: `index.html` — individual color properties across several CSS rules

Seven color values must change. Apply them one at a time.

- [ ] **Step 1: Update `.about-eyebrow` color**

Find:
```css
      color: var(--light-gold);
      margin-bottom: 1.25rem;
```
(Inside `.about-eyebrow` — the first occurrence of `var(--light-gold)` in the about section)

Replace with:
```css
      color: var(--gold);
      margin-bottom: 1.25rem;
```

- [ ] **Step 2: Update `.about-heading` color**

Find:
```css
      color: var(--light-text);
      margin-bottom: 1.5rem;
```
(Inside `.about-heading`)

Replace with:
```css
      color: var(--white);
      margin-bottom: 1.5rem;
```

- [ ] **Step 3: Update `.about-heading em` color**

Find:
```css
    .about-heading em {
      font-style: italic;
      color: var(--light-gold);
    }
```

Replace with:
```css
    .about-heading em {
      font-style: italic;
      color: var(--gold);
    }
```

- [ ] **Step 4: Update `.about-gold-rule` background**

Find:
```css
      background: var(--light-gold);
      opacity: 0.45;
      margin-bottom: 2rem;
```
(Inside `.about-gold-rule`)

Replace with:
```css
      background: var(--gold);
      opacity: 0.45;
      margin-bottom: 2rem;
```

- [ ] **Step 5: Update `.about-copy p` color**

Find:
```css
      color: var(--light-body);
      line-height: 1.9;
```
(Inside `.about-copy p`)

Replace with:
```css
      color: rgba(255,255,255,0.82);
      line-height: 1.9;
```

- [ ] **Step 6: Update `.about-pillars` border-top**

Find:
```css
      border-top: 1px solid rgba(201,146,42,0.18);
```
(Inside `.about-pillars`)

Replace with:
```css
      border-top: 1px solid rgba(255,255,255,0.14);
```

- [ ] **Step 7: Update `.pillar-label` color**

Find:
```css
      color: var(--light-text);
      letter-spacing: 0.01em;
```
(Inside `.pillar-label`)

Replace with:
```css
      color: var(--white);
      letter-spacing: 0.01em;
```

- [ ] **Step 8: Update `.pillar-sub` color**

Find:
```css
      color: var(--light-gold);
```
(Inside `.pillar-sub` — the last `var(--light-gold)` in the about section)

Replace with:
```css
      color: var(--gold);
```

- [ ] **Step 9: Verify no `--light-*` tokens remain in the about CSS block**

Search the file for `--light-` between the `/* ─── About` comment and the `/* ─── Contact` comment. Expected: zero matches.

---

## Task 6: Remove `.about-image` CSS block

**Files:**
- Modify: `index.html` lines 329–351

These four CSS rules are no longer needed once the image column is removed.

- [ ] **Step 1: Remove the `.about-image` CSS block**

Find this exact block:

```css
    .about-image { position: relative; }
    .about-image img {
      width: 100%;
      height: 580px;
      object-fit: cover;
      display: block;
    }
    .about-image-frame {
      position: absolute;
      top: -14px;
      right: -14px;
      bottom: 14px;
      left: 14px;
      border: 1px solid rgba(201,146,42,0.28);
      pointer-events: none;
    }
    .about-image::after {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(150deg, transparent 65%, rgba(201,146,42,0.04));
      pointer-events: none;
    }
```

Replace with: *(nothing — delete the block entirely)*

- [ ] **Step 2: Verify removal**

Search `index.html` for `.about-image`. Expected: zero matches.

---

## Task 7: Update HTML — add video and overlay, remove image column

**Files:**
- Modify: `index.html` lines 695–740

- [ ] **Step 1: Replace the About section HTML**

Find this exact block:

```html
  <!-- ── About ─────────────────────────────────────────── -->
  <section id="about" aria-labelledby="about-heading">
    <div class="about-inner">

      <div class="about-copy">
        <p class="about-eyebrow">Our Story</p>
        <h2 id="about-heading" class="about-heading reveal">
          Puerto Rico's Premier <em>Executive Carwash</em>
        </h2>
        <span class="about-gold-rule reveal" aria-hidden="true"></span>

        <p class="reveal">Executive Car Wash was born from a simple belief: that every driver in Puerto Rico deserves a world-class carwash experience — fast, effortless, and built for the island's climate and culture.</p>
        <p class="reveal">We built our tunnel around Sonny's industry-leading equipment, a full R.O. water filtration system, and a 50% water reclaim platform — because delivering excellence should never cost the earth.</p>
        <p class="reveal">From the moment you arrive to the moment you drive away spotless, every stage of our process is engineered to deliver a showroom-quality result in minutes, not hours.</p>

        <div class="about-pillars reveal">
          <div class="pillar-item">
            <span class="pillar-label">Speed</span>
            <span class="pillar-sub">Under 5 min</span>
          </div>
          <div class="pillar-sep" aria-hidden="true"></div>
          <div class="pillar-item">
            <span class="pillar-label">Luxury</span>
            <span class="pillar-sub">Sonny's systems</span>
          </div>
          <div class="pillar-sep" aria-hidden="true"></div>
          <div class="pillar-item">
            <span class="pillar-label">Sustain</span>
            <span class="pillar-sub">50% reclaim</span>
          </div>
        </div>
      </div>

      <div class="about-image reveal">
        <div class="about-image-frame" aria-hidden="true"></div>
        <img
          src="Brand Assets/Sequence Images/S9 Gemini 2.png"
          alt="Executive Car Wash tunnel exit — tropical Puerto Rico setting"
          width="600"
          height="580"
          loading="lazy"
        />
      </div>

    </div>
  </section>
```

Replace with:

```html
  <!-- ── About ─────────────────────────────────────────── -->
  <section id="about" aria-labelledby="about-heading">
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
    <div class="about-overlay" aria-hidden="true"></div>

    <div class="about-inner">
      <div class="about-copy">
        <p class="about-eyebrow">Our Story</p>
        <h2 id="about-heading" class="about-heading reveal">
          Puerto Rico's Premier <em>Executive Carwash</em>
        </h2>
        <span class="about-gold-rule reveal" aria-hidden="true"></span>

        <p class="reveal">Executive Car Wash was born from a simple belief: that every driver in Puerto Rico deserves a world-class carwash experience — fast, effortless, and built for the island's climate and culture.</p>
        <p class="reveal">We built our tunnel around Sonny's industry-leading equipment, a full R.O. water filtration system, and a 50% water reclaim platform — because delivering excellence should never cost the earth.</p>
        <p class="reveal">From the moment you arrive to the moment you drive away spotless, every stage of our process is engineered to deliver a showroom-quality result in minutes, not hours.</p>

        <div class="about-pillars reveal">
          <div class="pillar-item">
            <span class="pillar-label">Speed</span>
            <span class="pillar-sub">Under 5 min</span>
          </div>
          <div class="pillar-sep" aria-hidden="true"></div>
          <div class="pillar-item">
            <span class="pillar-label">Luxury</span>
            <span class="pillar-sub">Sonny's systems</span>
          </div>
          <div class="pillar-sep" aria-hidden="true"></div>
          <div class="pillar-item">
            <span class="pillar-label">Sustain</span>
            <span class="pillar-sub">50% reclaim</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

- [ ] **Step 2: Verify the HTML**

Read the About section in `index.html`. Confirm:
- `<video class="about-video-bg" ...>` is the first child of `#about`
- `<div class="about-overlay" ...>` follows the video
- `.about-inner` follows the overlay
- `.about-copy` is the only child of `.about-inner` (no `.about-image` div)
- All three paragraphs and the pillars are intact

---

## Task 8: Screenshot and visual verification

- [ ] **Step 1: Take the after screenshot**

```bash
node screenshot.mjs http://localhost:3000 after-about-video
```

- [ ] **Step 2: Read the screenshot**

Use the Read tool on the saved PNG. Verify all of the following:
1. The About section has a dark background (not cream/light)
2. The Corvette video is visible as the background (or dark fallback if browser sandbox blocks autoplay)
3. The text (eyebrow, heading, three paragraphs, three pillars) is centered and white/gold
4. There is no static image on the right side
5. The gold horizontal line is visible at the top of the section
6. The section is approximately full viewport height

- [ ] **Step 3: Check for any regressions above and below the About section**

Scroll the screenshot mentally — confirm the Packages section above and the Contact section below look unchanged. If any layout shift is visible, identify the cause before committing.

---

## Task 9: Commit

- [ ] **Step 1: Stage and commit**

```bash
git add index.html
git commit -m "feat: replace About section with Corvette cinematic video background"
```

Expected: commit succeeds, no errors.

- [ ] **Step 2: Confirm commit landed**

```bash
git log --oneline -3
```

Expected: The new commit appears at the top of the log.
