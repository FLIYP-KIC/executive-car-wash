# context.md — Executive Car Wash: Current Project State

_Last updated: 2026-04-24_

---

## Business

| Field | Value |
|---|---|
| Business name | Executive Car Wash |
| Location | Puerto Rico (exact address TBD) |
| Type | Automated tunnel carwash (conveyor rail, touchless + brush) |
| Tagline | Luxury · Rápido · Eficiente |
| Target market | Puerto Rico drivers seeking a premium, fast, automated wash |

---

## Site Overview

| Field | Value |
|---|---|
| Site type | Single-page marketing/landing site |
| Live URL | https://executivecarwashpr.com |
| Preview URL | https://executive-car-wash.vercel.app |
| Hosting | Vercel (free hobby tier) |
| Domain registrar | Vercel (domain purchased directly on Vercel) |
| GitHub repo | https://github.com/FLIYP-KIC/executive-car-wash |
| Deployment | Auto-deploy on every `git push` to `main` (via GitHub → Vercel integration) |

---

## Tech Stack

| Layer | Technology | Notes |
|---|---|---|
| HTML | Single `index.html` | All CSS and JS are inline — no build step |
| CSS framework | Tailwind CSS via CDN | Used sparingly for utility classes |
| Animation | GSAP 3.12.5 + ScrollTrigger via cdnjs CDN | Splash entrance, scroll reveals |
| Fonts | Cormorant Garamond + Inter | Loaded via Google Fonts CDN |
| Hosting | Vercel | Static site, global CDN |
| Version control | Git + GitHub | Repo: FLIYP-KIC/executive-car-wash |
| Local dev server | `serve.mjs` (Node.js) | Port 3000, handles URL-encoded paths and HTTP range requests |
| Screenshot tool | `screenshot.mjs` (Puppeteer) | Saves to `./temporary screenshots/`, auto-incremented |

---

## Page Structure

```
Splash Gate (fixed overlay, every page load)
  └─ Crown SVG + "Executive" wordmark + tagline + "Go Exec or Go Dirty" button

Navigation (fixed, z-index 1000)
  ├─ Left: Crown icon + "Executive" logo → links to #video-section
  ├─ Center: About · Contact (anchor links)
  └─ Right: "Due Diligence" dropdown button → 4 document downloads

§1 Video Section (100vh)
  └─ Brand Assets/Video.mp4 — autoplay, muted, loop, full viewport cover

§2 About (white/gold)
  ├─ Left: eyebrow + heading + gold rule + 3 body paragraphs + Speed·Luxury·Sustain pillars
  └─ Right: S9 Gemini 2.png (tropical tunnel exit image) with gold offset frame

§3 Contact (white/gold, continued)
  ├─ Centered header: "FIND US / Get in Touch"
  ├─ Left column: Location · Hours · Contact · Follow Us (all placeholder)
  └─ Right column: Name · Email · Message form + Send button (frontend-only, no backend)

Footer (white/gold)
  ├─ Left: "Executive Car Wash" italic + "Luxury · Rápido · Eficiente"
  ├─ Center: About · Contact links
  └─ Right: © 2026 Executive Car Wash. Puerto Rico.
```

---

## Design System

### Color Palette

| Token | Hex | Usage |
|---|---|---|
| `--bg` | `#0a0a0f` | Dark base (splash, nav background) |
| `--gold` | `#c9922a` | Primary accent — borders, labels, icons |
| `--gold-light` | `#f0c060` | Brand name, hover states, headings |
| `--light-bg` | `#fafaf8` | About, Contact, Footer backgrounds |
| `--light-text` | `#1a1a18` | Headings on white sections |
| `--light-body` | `#4a4a48` | Body copy on white sections |
| `--light-gold` | `#c9922a` | Gold accent on white sections |

### Typography

| Role | Font | Size / Weight |
|---|---|---|
| Brand / display headings | Cormorant Garamond | italic 700 for brand; 600 for section headings |
| Body / UI / labels | Inter | 400–800, varies by context |
| Splash brand name | Cormorant Garamond italic 700 | `clamp(3.5rem, 9vw, 8rem)` |
| Section headings | Cormorant Garamond 600 | `clamp(2.25rem, 3.5vw, 3.25rem)` |
| Eyebrow labels | Inter 500 | 0.56rem, 0.38em letter-spacing, uppercase |

---

## Brand Assets

| File | Size | Purpose | Status |
|---|---|---|---|
| `Brand Assets/Video.mp4` | 6.4 MB | Full-viewport autoplay video (tunnel journey) | In use |
| `Brand Assets/Sequence Images/S9 Gemini 2.png` | — | About section right-column image | In use |
| `Brand Assets/Exeecutive Car Wash Hero.jpeg` | 145 KB | Original hero image (no longer used) | Committed, unused |
| `Brand Assets/Sequence Images/S1–S8 Gemini 2.png` | — | AI reference images (not rendered) | Committed, unused |

---

## Business Documents (Due Diligence Downloads)

All files are served publicly from the project root. Accessible via the nav "Due Diligence" dropdown.

| File | Contents |
|---|---|
| `MCW_Construction_Cost_Model copy.xlsx` | Sonny's equipment schedule and construction costs |
| `PR_Car_Wash_Financial_Model copy.xlsx` | Financial model — blended $14.50/wash, 36% EBITDA base case |
| `PR_Car_Wash_Due_Diligence_Tracker copy.xlsx` | Due diligence tracking document |
| `PR_Car_Wash_Market_Intelligence_Report copy.docx` | Market research for Puerto Rico carwash market |

---

## Key Financial Data (from model)

| Metric | Conservative | Base | Optimistic |
|---|---|---|---|
| Cars/day | 153 | 250 | 361 |
| Blended revenue/wash | $13.00 | $14.50 | $15.50 |
| EBITDA margin | 17% | 36% | 41% |

---

## Placeholder Content (needs real data)

- Business address (contact section shows "Address — Coming Soon")
- Phone number (currently `(787) 000-0000`)
- Email (currently `info@executivecarwashpr.com` — needs to be a real inbox)
- Instagram, Facebook, TikTok handles (currently `#` links)
- About Us copy (currently well-written placeholder — needs owner's real story)
