# decisions.md — Key Architecture & Design Decisions

_Last updated: 2026-04-24_

Each entry records what was decided, why, and what was ruled out. This prevents relitigating the same choices in future sessions.

---

## Architecture

### Single `index.html` — No Build Step
**Decision:** All HTML, CSS, and JavaScript live in one file. No Node.js, no React, no bundler.
**Why:** The site is a marketing landing page, not an app. A build pipeline adds complexity with zero benefit here. Any developer (or AI) can open one file and understand the entire site instantly.
**Ruled out:** React/Next.js, Astro, Vite — all overkill for a single-page brochure site.

---

### Tailwind CSS via CDN
**Decision:** Load Tailwind from the CDN script tag rather than installing it as a package.
**Why:** Consistent with the no-build-step decision. Tailwind is used sparingly for layout utilities — the primary styling is done through CSS custom properties in the `<style>` block.
**Ruled out:** PostCSS build, `@tailwind` directives — require a build step.

---

### GSAP + ScrollTrigger via CDN
**Decision:** Load GSAP 3.12.5 and ScrollTrigger from cdnjs.
**Why:** GSAP is the industry standard for web animation. ScrollTrigger handles scroll-based reveals cleanly. CDN delivery keeps the no-build approach intact.
**Ruled out:** CSS-only animations (insufficient control), custom scroll listeners (reinventing the wheel), Framer Motion (React-only).

---

### Vercel for Hosting
**Decision:** Deploy to Vercel, domain also registered through Vercel.
**Why:** Zero-configuration static hosting, global CDN, free tier, automatic HTTPS, one-click rollbacks, and direct domain registration means no DNS configuration required.
**Ruled out:** GitHub Pages (requires custom DNS setup, no range request support for video), Netlify (equally good, but Vercel was set up first), AWS S3 (overkill, requires DevOps knowledge).

---

### GitHub → Vercel Auto-Deploy
**Decision:** Connect the GitHub repository to Vercel so every `git push` triggers an automatic production deployment.
**Why:** Removes the manual step of running `vercel --prod` after every change. All changes are version-controlled and reversible via Vercel's deployment history.
**Ruled out:** CLI-only deployment (manual, easy to forget, no history beyond git log).

---

## Design

### Dual-Theme Palette (Dark Splash/Nav + White/Gold Content)
**Decision:** The splash screen and navigation are dark (`#0a0a0f` base, gold accents). The About, Contact, and Footer sections are white (`#fafaf8`) with gold accents.
**Why:** The dark entry creates a dramatic, cinematic luxury first impression. The white content sections make the copy highly readable and feel premium — consistent with luxury jewelry and hotel brands. The gold thread connects both themes.
**Ruled out:** All-dark site (harder to read body copy at length), all-light site (loses the cinematic entrance feel).

---

### Splash Gate on Every Page Load
**Decision:** The splash screen appears every time the page loads, with no `sessionStorage` persistence.
**Why:** Owner explicitly requested this behavior. The splash is the brand moment — "Go Exec or Go Dirty" is the hook. Re-showing it on every visit reinforces the brand voice.
**Ruled out:** Show once per session (rejected by owner), show once per browser visit with `localStorage` (rejected by owner).

---

### Video Autoplay (No Scroll Scrubbing)
**Decision:** `Brand Assets/Video.mp4` plays as a full-viewport autoplay loop. No GSAP ScrollTrigger scrubbing.
**Why:** The original scroll-driven video (800vh pinned section, 9 stage overlays) was complex and the owner simplified the vision — "start the video right away, no scroll factor." Autoplay after splash dismiss gives the cinematic moment without requiring scroll interaction.
**Ruled out:** Scroll-scrubbed video (original build — removed in v2), sequence image crossfade (rejected by owner in favor of video).

---

### Removed Sections: Packages & Memberships
**Decision:** The Packages ($13/$18/$24) and Memberships (monthly/yearly toggle) sections were removed entirely.
**Why:** Owner requested a cleaner, simpler site focused on brand impression. Pricing and membership details will be handled operationally (at the physical location) rather than on the landing page.
**Ruled out:** Keeping pricing on the site — explicitly removed by owner request.
**Note:** Pricing data still exists in `PR_Car_Wash_Financial_Model copy.xlsx` and can be added back to the site at any time.

---

### Due Diligence Dropdown in Navigation
**Decision:** Business documents (4 Excel/Word files) are accessible via a "Due Diligence" button in the top-right nav that opens a dropdown panel.
**Why:** The site serves a dual audience — potential customers AND potential investors. The dropdown provides clean investor access without cluttering the main page experience for customers.
**Ruled out:** Separate investor page (adds routing complexity), in-body section (disrupts the customer-facing flow), password-protected (adds backend complexity, documents are acceptable to share via URL).

---

### Cormorant Garamond + Inter Font Pairing
**Decision:** Cormorant Garamond (display/brand) paired with Inter (body/UI).
**Why:** Cormorant brings editorial luxury — the italic weight on "Executive" is distinctive and memorable. Inter is the most legible modern sans-serif at small sizes, ideal for UI labels and body copy. This pairing is used by high-end hospitality and jewelry brands.
**Ruled out:** All-sans (loses the luxury personality), Playfair Display (too common), system fonts (generic).

---

### Contact Form — Frontend Only
**Decision:** The contact form validates and shows a success message but does not send data anywhere. No backend is connected.
**Why:** Getting the site live quickly was the priority. A form backend (email service) is a separate task that requires credentials and a provider decision.
**Impact:** Submissions are currently silently discarded. This must be resolved before the site is shared publicly.
**Planned fix:** Connect to Formspree or EmailJS (no backend server required — see `next_steps.md`).

---

### About Section Image — S9 Gemini 2.png
**Decision:** Use the AI-generated S9 reference image (tropical tunnel exit scene with Audi Q8) as the About section's right-column image.
**Why:** It's the most visually compelling asset available — shows a luxury car exiting into a tropical setting, directly communicating the Puerto Rico context and the quality of the experience.
**Future:** Replace with real photography of the actual facility when it opens.
