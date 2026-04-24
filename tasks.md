# tasks.md — In Progress & Outstanding Work

_Last updated: 2026-04-24_

---

## Status Legend
- 🟢 **Done** — complete and live
- 🟡 **In Progress** — started, not yet complete
- 🔴 **Blocked** — waiting on owner input or external action
- ⚪ **Queued** — planned, not yet started

---

## Infrastructure

| Status | Task | Notes |
|---|---|---|
| 🟢 | Git repository initialized | Local + pushed to GitHub |
| 🟢 | GitHub repo created | `FLIYP-KIC/executive-car-wash` |
| 🟢 | Vercel project created | `executive-car-wash` |
| 🟢 | Domain purchased | `executivecarwashpr.com` via Vercel |
| 🟡 | GitHub → Vercel auto-deploy connected | Owner needs to link in Vercel dashboard: Settings → Git → Connect Repository |
| 🟢 | `vercel.json` configured | Video range requests, xlsx/docx download headers |
| 🟢 | `.gitignore` configured | Excludes node_modules, screenshots, dev tools |

---

## Site Build

| Status | Task | Notes |
|---|---|---|
| 🟢 | Splash gate | Dark luxury, crown, "Go Exec or Go Dirty" CTA, GSAP entrance animation |
| 🟢 | Navigation | Logo + About/Contact links + Due Diligence dropdown |
| 🟢 | Due Diligence dropdown | 4 document downloads, open/close on click, closes on Escape/outside click |
| 🟢 | Video section | Autoplay, muted, loop, full viewport — plays on splash dismiss |
| 🟢 | About section | White/gold, asymmetric layout, S9 image, pillars, placeholder copy |
| 🟢 | Contact section | White/gold, centered header, info column, contact form |
| 🟢 | Footer | White/gold, brand, links, copyright |
| 🟢 | Scroll reveal animations | `.reveal` class — GSAP fade-up on scroll |

---

## Content Gaps (Owner Must Provide)

| Status | Task | What's needed |
|---|---|---|
| 🔴 | Real business address | Physical location in Puerto Rico |
| 🔴 | Real phone number | Replace `(787) 000-0000` |
| 🔴 | Real email inbox | Replace `info@executivecarwashpr.com` with working inbox |
| 🔴 | Social media handles | Instagram, Facebook, TikTok account URLs |
| 🔴 | About Us copy | Owner's real origin story and mission (2–3 paragraphs) |
| 🔴 | Hours confirmation | Currently shows Mon–Sun 7AM–9PM — confirm or correct |

---

## Pending Technical Work

| Status | Task | Priority | Notes |
|---|---|---|---|
| ⚪ | Contact form backend | HIGH | Form currently has no backend — submissions go nowhere. Needs Formspree, EmailJS, or similar |
| ⚪ | Mobile navigation | MEDIUM | Nav links hidden on mobile (< 768px). Needs a hamburger menu |
| ⚪ | Favicon | MEDIUM | No favicon set — browser shows default blank tab icon |
| ⚪ | Open Graph meta tags | MEDIUM | No OG tags — links shared on WhatsApp/iMessage show no preview image or title |
| ⚪ | Google Analytics | LOW | No tracking installed — can't see visitor traffic |
| ⚪ | Verify live video on Vercel | HIGH | Video.mp4 needs to be confirmed playing on the live domain (CDN range request support) |
