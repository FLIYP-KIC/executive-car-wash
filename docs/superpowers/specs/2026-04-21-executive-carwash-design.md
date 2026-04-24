# Executive Car Wash — Landing Page Design Spec

**Date:** 2026-04-21  
**Status:** Approved  
**Location:** Puerto Rico  
**Business type:** Automated tunnel carwash  

---

## 1. Business Overview

| Field | Value |
|---|---|
| Business name | Executive Car Wash |
| Location | Puerto Rico |
| Carwash type | Automated tunnel (conveyor rail, touchless + brush) |
| Services | Basic / Premium / Ultimate single-wash tiers |
| Subscription | Monthly and yearly unlimited membership plans |
| Tagline | Luxury · Rápido · Eficiente |

---

## 2. Visual Direction

### Palette

| Role | Hex | Usage |
|---|---|---|
| Background deep | `#0a0a0f` | Page base, hero |
| Background elevated | `#141428` | Section surfaces, cards |
| Gold primary | `#c9922a` | Borders, icons, accents |
| Gold highlight | `#f0c060` | Brand name, CTAs, hover states |
| White | `#ffffff` | Body text, headings |
| White muted | `rgba(255,255,255,0.55)` | Secondary copy |

### Typography

| Role | Font | Style |
|---|---|---|
| Brand name "Executive" | Cormorant Garamond | Italic, 700, gold, large |
| Sub-brand "CAR WASH" | Inter | 800, letter-spacing 0.18em, white caps |
| Section headings | Cormorant Garamond | 600, mixed case |
| Body / UI | Inter | 400–500, white/muted |
| Stage labels (tunnel) | Inter | 300, wide-tracked caps, gold |

### Iconography
- Crown symbol above the brand name (SVG, gold)
- Minimal line icons for features/perks

### Atmosphere
- Deep black/navy base — no light backgrounds anywhere
- Gold as the single accent color — used sparingly for hierarchy
- Tropical night mood: references S1 and S9 assets (palm trees, bougainvillea, wet asphalt reflections)
- Layered depth: dark base → slightly lighter cards → floating elements
- Grain/noise texture layer at low opacity for premium feel

---

## 3. Brand Assets

All assets live in `Brand Assets/`.

### Hero Image
- `Brand Assets/Exeecutive Car Wash Hero.jpeg` — Aerial dusk shot of a real Executive Carwash facility: modern grey building, blue "executive carwash" wave logo, glass storefront, multiple vehicles on site. Used as the §1 Hero section background. Apply `rgba(0,0,0,0.60)` dark overlay + gold color treatment to align with dark luxury direction.

### Tunnel Video (primary animation source)
- `Brand Assets/Video.mp4` — Full-motion carwash tunnel journey. Scrubbed frame-by-frame via GSAP ScrollTrigger. The scroll progress (0→1) maps to video currentTime (0 → video.duration). Text overlays appear at defined scroll breakpoints, synchronized to video content.

### Sequence Images (reference only — NOT used in animation)
- `Brand Assets/Sequence Images/S1–S9 Gemini 2.png` — Available as reference for overlay timing/copywriting. Not rendered in the page.

---

## 4. Page Architecture

Single `index.html` file. All styles inline or in a `<style>` block. Tailwind CSS via CDN. GSAP + ScrollTrigger via CDN.

### Section Map

```
┌─────────────────────────────────────────────┐
│  §1  HERO          100vh                    │
│      Brand entrance · CTA                  │
├─────────────────────────────────────────────┤
│  §2  TUNNEL JOURNEY  ~800vh pinned          │
│      9-stage image sequence · overlays      │
│      S1 → S2 → S3 → S4 → S5 →             │
│      S6 → S7 → S8 → S9                     │
├─────────────────────────────────────────────┤
│  §3  PACKAGES       auto                   │
│      Basic · Premium · Ultimate             │
├─────────────────────────────────────────────┤
│  §4  MEMBERSHIPS    auto                   │
│      Monthly · Yearly toggle · perks        │
├─────────────────────────────────────────────┤
│  §5  ABOUT US       auto                   │
│      Story · Puerto Rico · values           │
├─────────────────────────────────────────────┤
│  §6  CONTACT + FOOTER  auto                │
│      Location · hours · form · socials      │
└─────────────────────────────────────────────┘
```

---

## 5. Section Specs

### §1 — Hero
- Full viewport (100vh), overflow hidden
- Background: `Brand Assets/Exeecutive Car Wash Hero.jpeg` as full-bleed cover image, darkened with `rgba(0,0,0,0.60)` overlay + subtle gold radial gradient tint for luxury alignment
- Center-aligned content stack:
  - Crown SVG icon (gold, ~48px, animates down from y:-20 on load)
  - "Executive" in Cormorant Garamond italic gold (~clamp(5rem,10vw,9rem))
  - "CAR WASH" in Inter wide-tracked white caps
  - Thin gold divider line (60px wide)
  - "LUXURY · RÁPIDO · EFICIENTE" in Inter small caps, gold/muted
  - "Puerto Rico's Premier Express Carwash" — body copy, white/55%
  - CTA: "Begin the Experience" button — gold border, transparent fill, hover fills gold
- Sticky navigation bar: logo left, anchor links right (Packages · Memberships · About · Contact)
- Entrance animation: all elements stagger in (opacity 0→1, y 30→0) on page load via GSAP

### §2 — Tunnel Journey (Scroll-Driven Video)
- Container pinned via GSAP ScrollTrigger for ~800vh of scroll distance
- `<video>` element: `Brand Assets/Video.mp4`, muted, preload="auto", no autoplay, `object-fit: cover`, full viewport
- Scroll progress (0→1) maps to `video.currentTime` (0 → video.duration) via `onUpdate` callback
- Text overlays are NOT tied to image crossfades — they are tied to **scroll progress breakpoints** defined below
- Each overlay fades in (opacity 0→1, y 15→0) at its `start` threshold and fades out at its `end` threshold
- Scroll progress bar: thin gold vertical line on left edge, height = scroll %
- Stats bar: fixed bottom strip showing live business stat relevant to current stage (gold text on dark translucent bar)

### Video Scroll Overlay Copy & Data Points
*(Scroll progress 0.0–1.0 divided into 9 bands of ~0.111 each)*

| Band | Progress | Label | Headline | Copy | Data Stat (bottom bar) |
|---|---|---|---|---|---|
| 1 | 0.00–0.11 | WELCOME TO EXECUTIVE | Your journey begins here | Pull up, select your wash, and let us take it from here. | 250+ cars served daily |
| 2 | 0.11–0.22 | ENTERING THE TUNNEL | Step into the experience | Our precision conveyor guides you safely through every stage. | 130-ft tunnel · Sonny's conveyor system |
| 3 | 0.22–0.33 | PRE-SOAK TREATMENT | High-pressure pre-rinse | Powerful jets loosen road grime before the wash even begins. | D-10 high-pressure pump system |
| 4 | 0.33–0.44 | EXECUTIVE FOAM BLAST | Triple-action foam application | Our signature foam clings and lifts even the toughest buildup. | Bug Cleaner G-57 + triple-foam applicator |
| 5 | 0.44–0.55 | OMNI BRUSH SYSTEM | Wrap-around precision cleaning | Sonny's Omni 150 side + Omni 350 top brushes contour every surface. | Omni 150 side · Omni 350 top · PM-28P side brush |
| 6 | 0.55–0.66 | WHEEL BLASTER | Rim-to-rim clean | The SP100 Wheel Blaster spinner targets every spoke and rim edge. | SP100 Wheel Blaster · Tire Brush PP |
| 7 | 0.66–0.77 | R.O. SPOT-FREE RINSE | Reverse osmosis filtered water | Purified water leaves zero mineral deposits — a truly spot-free finish. | R.O. Filtration System · Water Softener |
| 8 | 0.77–0.88 | TIRE SHINE & DRY | Showroom finish, every time | Tire dressing + 64 CFM air dryers eliminate water before you exit. | Air Dryer 64 CFM · Tire Dressing PP |
| 9 | 0.88–1.00 | SPOTLESS. EVERY TIME. | Welcome back to Puerto Rico | Clean car. Clear skies. Ready for whatever comes next. | $14.50 avg · 36% EBITDA · Puerto Rico's Premier Wash |

### §3 — Packages
- Section heading: "Choose Your Wash" (Cormorant Garamond, gold)
- 3 cards in a row (responsive: stack on mobile):
  - **Basic** — standard border, white heading
  - **Premium** — gold border, gold "Most Popular" badge
  - **Ultimate** — gold border + glow shadow, crown icon
- Each card: wash name, price, feature list (checkmarks), CTA button

**Placeholder pricing** (from financial model blended revenue $13–$15.50/wash):

| Tier | Price | Equipment Highlights |
|---|---|---|
| Basic | $13 | Pre-soak · Foam blast · High-pressure rinse · Air dry |
| Premium | $18 | All Basic + Omni brush system · Wheel Blaster SP100 · Tire shine |
| Ultimate | $24 | All Premium + R.O. spot-free rinse · Ceramic wax · Tire dressing · Triple foam |

### §4 — Memberships
- Toggle: Monthly | Yearly (yearly shows savings callout, e.g. "Save 20%")
- 2 plan cards per tier × 2 billing cycles = toggled display
- Member perks list below cards (e.g. unlimited washes, priority lane, monthly ceramic, etc.)
- CTA: "Join the Club" button

### §5 — About Us
- Two-column layout: copy left, image right (S9 exit reveal image)
- Headline: "Puerto Rico's Premier Executive Carwash"
- 2–3 paragraphs: origin story, mission, community commitment
- 3 value pillars with gold icon + label: Speed · Luxury · Sustainability
- Puerto Rico flag accent or map element

### §6 — Contact + Footer
- Location address
- Operating hours (to be provided)
- Phone and email
- Simple contact form: Name · Email · Message · Send
- Social media links (Instagram, Facebook, TikTok — to be confirmed)
- Footer: copyright, nav links, tagline

---

## 6. Animation System

### Libraries (CDN)
```html
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
```

### Rules
- Only animate `transform` and `opacity` (per CLAUDE.md)
- Never `transition-all`
- Easing: `power2.out` for reveals, `power3.inOut` for stage transitions
- Respect `prefers-reduced-motion` — disable non-essential motion

### Key Timelines
- `heroRevealTl` — staggered entrance on load (crown → brand name → tagline → CTA)
- `tunnelScrollTl` — ScrollTrigger pin + image crossfade + overlay text per stage
- `sectionRevealTl` — per-section fade-up as they enter viewport

---

## 7. File Structure

```
/
├── index.html                          # Entire site, single file
├── serve.mjs                           # Local dev server (port 3000) — CREATE IN PHASE 1
├── screenshot.mjs                      # Puppeteer screenshot utility — CREATE IN PHASE 1
├── CLAUDE.md                           # Project-level AI instructions
├── Brand Assets/
│   ├── Exeecutive Car Wash Hero.jpeg   # Hero section background image
│   ├── Video.mp4                       # Tunnel scroll animation source
│   └── Sequence Images/               # Reference only — not rendered
│       └── S1–S9 Gemini 2.png
├── MCW_Construction_Cost_Model copy.xlsx
├── PR_Car_Wash_Financial_Model copy.xlsx
├── PR_Car_Wash_Due_Diligence_Tracker copy.xlsx
├── PR_Car_Wash_Market_Intelligence_Report copy.docx
└── docs/
    └── superpowers/
        └── specs/
            └── 2026-04-21-executive-carwash-design.md
```

**Note on CLAUDE.md:** The `screenshot.mjs` Puppeteer path references a Windows path (`C:/Users/nateh/...`). This project is on macOS — update the path to use the system-installed Chromium when creating `screenshot.mjs`.

---

## 8. Skills Required (Build Order)

| Phase | Skill | Purpose |
|---|---|---|
| Before any code | `/frontend-design` | Mandatory per CLAUDE.md — sets frontend standards |
| Design quality check | `/gpt-taste` | Visual quality review before shipping each section |
| Implementation | `/plan` | Break build into implementation tasks |
| After each section | `/code-review` | Catch issues early per section |
| After contact form | `/security-review` | Validate form handling and any data exposure |
| Final | `/e2e` | End-to-end scroll experience verification |
| Final | `/verify` | Confirm all spec requirements are met |

---

## 9. Outstanding Information Needed

The following will be needed before the corresponding sections can be finalized:

- [ ] Wash package pricing (Basic / Premium / Ultimate)
- [ ] Feature list per wash tier (from parts/equipment list)
- [ ] Membership pricing (monthly / yearly per tier)
- [ ] Member perks list
- [ ] Business address and operating hours
- [ ] Phone number and email
- [ ] Social media handles (Instagram, Facebook, TikTok)
- [ ] About Us copy / origin story
- [ ] Logo (or confirm we design the crown + wordmark from scratch in code)

---

## 10. CLAUDE.md Notes

Per the project `CLAUDE.md`:
- **Always invoke `/frontend-design`** before writing any frontend code
- Serve via `node serve.mjs` at `localhost:3000`
- Screenshot via `node screenshot.mjs http://localhost:3000`
- Brand assets are in `Brand Assets/` (note: capital B, capital A, with space — not `brand_assets/`)
- No default Tailwind palette — use the gold/black palette defined above
- Layered shadows, grain texture, spring easing — see CLAUDE.md anti-generic guardrails
- Every interactive element needs hover + focus-visible + active states
