# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Always Do First
- **Invoke the `frontend-design` skill** before writing any frontend code, every session, no exceptions.

## Project: Executive Car Wash

Single-page luxury landing page for an automated tunnel carwash in Puerto Rico.

**Architecture:** Single `index.html` (all CSS + JS inline). No build step. Tailwind CDN + GSAP CDN.

**Sections (in order):**
1. Sticky nav — logo left, anchor links right
2. Hero — full-viewport, `Brand Assets/Exeecutive Car Wash Hero.jpeg` background (note: double 'e' in filename)
3. Tunnel Journey — 800vh pinned scroll, `Brand Assets/Video.mp4` scrubbed via GSAP ScrollTrigger
4. Packages — Basic $13 / Premium $18 / Ultimate $24 (3-card layout)
5. Memberships — monthly/yearly toggle, JS price swap
6. About Us — two-column, S9 static image right
7. Contact + Footer — honeypot form, address/hours/socials TBD

**Palette:** `#0a0a0f` base · `#c9922a` gold · `#f0c060` gold-light · `rgba(255,255,255,0.55)` muted
**Fonts:** Cormorant Garamond (display) + Inter (body/UI) — both from Google Fonts CDN

**Tunnel scroll mechanics:**
- `#tunnel-wrapper` at `height:800vh`; `#tunnel-sticky` at `position:sticky; top:0; height:100vh`
- `video.currentTime = self.progress * video.duration` via ScrollTrigger `onUpdate`
- 9 stage overlays keyed to scroll progress bands (0.0–0.11, 0.11–0.22, … 0.88–1.0)
- iOS Safari fallback: `canScrubVideo()` checks `video.seekable`; if video fails, overlays still animate

**Key data files** (reference only — not rendered):
- `MCW_Construction_Cost_Model copy.xlsx` — Sonny's equipment schedule
- `PR_Car_Wash_Financial_Model copy.xlsx` — financial model (blended $14.50/wash, 36% EBITDA base)
- `PR_Car_Wash_Market_Intelligence_Report copy.docx` — market research
- `Brand Assets/Sequence Images/` — AI reference images, NOT used in animations

## Local Server

```bash
node serve.mjs          # starts http://localhost:3000
```

- Serves project root at port 3000
- Handles URL-decoded paths (required for `Brand Assets/` filenames with spaces)
- Supports HTTP range requests (required for video scrubbing)
- If port 3000 is in use: `lsof -ti:3000 | xargs kill -9`

## Screenshot Workflow

```bash
node screenshot.mjs http://localhost:3000          # saves screenshot-N.png
node screenshot.mjs http://localhost:3000 label    # saves screenshot-N-label.png
```

- Puppeteer uses the system-installed Chromium (macOS, no hardcoded path)
- Screenshots saved to `./temporary screenshots/` (auto-incremented, never overwritten)
- After screenshotting, read the PNG with the Read tool to analyze it
- Always screenshot from localhost, never from `file:///`
- Check: spacing/padding, font size/weight, exact hex colors, alignment, border-radius, shadows

## Brand Assets

The folder is named `Brand Assets/` — capital B, capital A, with a space. Never `brand_assets/`.

| File | Usage |
|------|-------|
| `Brand Assets/Exeecutive Car Wash Hero.jpeg` | Hero section background (note double 'e') |
| `Brand Assets/Video.mp4` | Tunnel scroll animation (GSAP scrubbing) |
| `Brand Assets/Sequence Images/` | Reference only — not rendered on page |

## Output Defaults
- Single `index.html` file, all styles and scripts inline
- Tailwind CSS via CDN: `<script src="https://cdn.tailwindcss.com"></script>`
- GSAP 3.12.5 + ScrollTrigger via cdnjs CDN
- Mobile-first responsive

## Reference Images
- If a reference image is provided: match layout, spacing, typography, and color exactly. Swap in placeholder content. Do not improve or add to the design.
- Screenshot output, compare against reference, fix mismatches, re-screenshot. At least 2 comparison rounds. Stop only when no visible differences remain or user says so.

## Anti-Generic Guardrails
- **Colors:** Never use default Tailwind palette. Use the gold/black palette defined above.
- **Shadows:** Never flat `shadow-md`. Use layered, color-tinted shadows with low opacity.
- **Typography:** Cormorant Garamond for display, Inter for body. Tight tracking on large headings, generous line-height on body.
- **Gradients:** Layer multiple radial gradients. Add grain via SVG noise filter (`body::before`).
- **Animations:** Only `transform` and `opacity`. Never `transition-all`. Spring-style easing.
- **Interactive states:** Every clickable element needs hover, focus-visible, and active states.
- **Images:** Gradient overlay + color treatment via `mix-blend-multiply`.
- **Depth:** Base → elevated → floating surface system.

## Hard Rules
- Do not add sections not in the spec
- Do not "improve" a reference design — match it
- Do not stop after one screenshot pass
- Do not use `transition-all`
- Do not use default Tailwind blue/indigo as primary color
