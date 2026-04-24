# next_steps.md — Exact Next Actions

_Last updated: 2026-04-24_

Ordered by priority. Items marked **[OWNER]** require information or action from you. Items marked **[CLAUDE]** can be executed in a future session without any input needed.

---

## 🔴 Immediate (Before Sharing the Site Publicly)

### 1. Connect GitHub to Vercel Auto-Deploy [OWNER — 2 min]
Without this, changes won't deploy automatically.
1. Go to vercel.com → executive-car-wash project
2. Settings → Git → Connect Git Repository
3. Select GitHub → choose `FLIYP-KIC/executive-car-wash`
4. Click Connect

---

### 2. Verify Video Plays on the Live Domain [OWNER — 5 min]
Open `https://executivecarwashpr.com` in a browser, dismiss the splash, and confirm the tunnel video autoplays. If it shows a black screen, report back — it means the CDN isn't serving the range request headers correctly and I'll fix `vercel.json`.

---

### 3. Fix the Contact Form — Connect to a Real Email [CLAUDE — 30 min]
Currently the form accepts input but sends nothing. Easiest free solution: **Formspree**.
- You create a free account at formspree.io
- They give you a form endpoint URL (looks like `https://formspree.io/f/xxxxxxxx`)
- I update 3 lines in `index.html` and push — submissions go straight to your email inbox
- No server needed, free up to 50 submissions/month

**What I need from you:** Confirm you want Formspree (or name another preference) and create the account. I handle the rest.

---

## 🟡 High Priority (Do This Week)

### 4. Fill In Real Contact Information [OWNER — provides data, CLAUDE — implements]
Provide the following and I'll update the site and push in one go:
- [ ] Business address (street, city, Puerto Rico, zip)
- [ ] Real phone number
- [ ] Real email address for the inbox
- [ ] Instagram handle / URL
- [ ] Facebook page URL
- [ ] TikTok handle / URL
- [ ] Confirm hours (currently Mon–Sun 7AM–9PM)

---

### 5. Add a Favicon [CLAUDE — 15 min]
Currently the browser tab shows a blank icon. A simple gold crown SVG favicon would complete the brand presence.
No input needed — I can generate this from the existing crown SVG in the site.

---

### 6. Add Open Graph Meta Tags [CLAUDE — 20 min]
When someone shares `executivecarwashpr.com` on WhatsApp, iMessage, or Instagram, it currently shows no preview image, no title, nothing — just a bare link.
Adding OG tags means it will display:
- A preview image (the tunnel video thumbnail or a still)
- Title: "Executive Car Wash — Puerto Rico's Premier Express Carwash"
- Description: "Luxury · Rápido · Eficiente"

**What I need from you:** A still image to use as the share preview (JPG, ideally 1200×630px). Can use the hero JPEG we have if you don't have another.

---

## ⚪ Medium Priority (Do This Month)

### 7. Mobile Navigation — Hamburger Menu [CLAUDE — 45 min]
On screens under 768px, the nav links (About, Contact) are hidden. The Due Diligence button is also cramped. A hamburger menu opens a full-screen mobile nav.
No input needed — can be done in a future session.

---

### 8. Write Real About Us Copy [OWNER — provides story, CLAUDE — formats]
The current 3 paragraphs are well-crafted placeholders but they're not your story. When you're ready, share:
- How the idea started
- Your background / why Puerto Rico
- What makes Executive different from other carwashes
I'll refine it to match the luxury tone of the site.

---

### 9. Add Google Analytics [CLAUDE — 20 min]
Lets you see how many people visit, where they come from, and which sections they spend time on.
**What I need from you:** Create a free Google Analytics 4 property at analytics.google.com and give me the Measurement ID (looks like `G-XXXXXXXXXX`). I add one line to `index.html`.

---

## ⚪ Lower Priority (Future Enhancements)

### 10. Real Photography [OWNER — external]
Replace the AI-generated S9 image in the About section with real photos of the facility, team, or the tunnel in action. Professional photography will significantly increase trust for potential customers.

### 11. Packages & Pricing Section [CLAUDE — if needed]
The Basic ($13) / Premium ($18) / Ultimate ($24) pricing section was removed at owner's request. It can be re-added at any time once pricing is finalized and the owner wants it on the site.

### 12. Spanish Language Toggle [CLAUDE — 2–3 hours]
Puerto Rico is bilingual. Adding an EN/ES toggle on the nav lets visitors switch the full site to Spanish. Significant effort but high value for the local market.

### 13. Online Booking / Pre-Pay [OWNER decision + CLAUDE — integration]
A "Book a Wash" or "Pre-Pay Online" button connected to a payment processor (Square, Stripe) would let customers purchase before arriving. Requires business decisions on operational readiness before implementation.

---

## How Updates Work Going Forward

1. Tell me what to change in this chat
2. I edit `index.html` (or other files) and run:
   ```bash
   git add . && git commit -m "description" && git push
   ```
3. Vercel detects the push and deploys automatically within ~60 seconds
4. Change is live at `executivecarwashpr.com`

No Terminal work needed from you after the GitHub → Vercel connection is set up.
