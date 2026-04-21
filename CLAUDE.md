# andreea-cover — Claude Code Instructions

## Project Overview
Single-page personal cover site for **Andreea Bîndar**, UX/Product Designer.
Deployed via GitHub Pages at `cover.andreeabindar.se`.
Single file: `index.html` — all CSS, JS, and base64 assets are inline.

## Core Stack
- Pure HTML/CSS/JS — no framework, no build step
- Fonts: DM Serif Display (headings) + DM Sans (body) via Google Fonts
- All assets (photo, CV PDF) embedded as base64 — no external file references
- Deployed: push to `main` → GitHub Pages auto-deploys in ~60 seconds

## Design System

### Colors
```
--cream: #FAF8F4        /* page background */
--warm-white: #FFFEF9   /* card surfaces */
--ink: #1A1814          /* primary text */
--ink-mid: #4A4640      /* secondary text */
--ink-light: #8A8480    /* muted text */
--accent: #C4713A       /* section labels, borders */
--accent-light: #F0E4D8 /* tag backgrounds */
--orange: #E8560A       /* primary CTA, nav button */
--orange-dark: #B8430A  /* CTA hover state */
--border: rgba(26,24,20,0.10)
```

### Typography Scale (Major Third 1.25 ratio)
- Hero name: clamp(38px, 7vw, 58px) — DM Serif Display
- Section titles: 28px — DM Serif Display
- Project name: 22px — DM Serif Display
- Body: 16px / line-height 1.65 — DM Sans weight 300
- Small/labels: 13–14px — DM Sans weight 400–500
- Eyebrow labels: 11–12px uppercase, letter-spacing 0.10em

### Spacing (8pt grid)
- Section padding: 72px 24px
- Card padding: 18–28px
- Component gaps: 8, 10, 12, 16, 24px
- Mobile section padding: 48px 20px

### Border Radius
- Cards: 12–16px
- Buttons: 100px (pill)
- Tags/pills: 20px
- Photo frame: 50% (circle)

## CTA Hierarchy (UX Laws — do not break these)
1. **Primary** (`btn-primary`): orange fill `#E8560A`, 48px min-height, one per section max — Hick's Law
2. **Secondary** (`btn-text`): text link with underline on hover, clearly subordinate
3. **Nav CTA** (`.nav-cta`): orange outline, ghost style — present but not competing
4. **Footer links**: plain text, low visual weight

**Rule:** Never place two filled buttons side by side. Never more than one primary CTA per section.

## Sections (in order)
1. **Hero** — photo + name + tagline + primary CTA (game) + secondary links (CV, portfolio)
2. **Vad jag erbjuder** (`#hjalper`) — 2x2 card grid of services
3. **Omaia project** (`#projekt`) — single project card with pills
4. **Nästa steg** (`#soker`) — 3-row seek table
5. **Vanliga frågor** (`#faq`) — 4 FAQ items
6. **Final CTA** — quote + "Connect with me" LinkedIn button + secondary links

## Key Links
- Game: `https://doyouknowme.andreeabindar.se/` — opens in **same tab** (enables swipe back on mobile)
- Portfolio: `https://andreeabindar.se/` — same tab
- LinkedIn: `https://www.linkedin.com/in/andreea-bindar/` — same tab for nav + final CTA
- Email: `andreealb62@gmail.com`
- CV: embedded as base64, downloaded via Blob URL

## Accessibility Requirements
- Skip link at top (`<a href="#main-content">`)
- All sections use `<section>` with `aria-label`
- Nav has `role="navigation" aria-label="Huvudnavigation"`
- All SVG icons have `aria-hidden="true"`
- `prefers-reduced-motion` respected — no animations when set
- Focus states: `2px solid #E8560A` outline, `outline-offset: 3px`
- Minimum touch targets: 44px height on all interactive elements
- WCAG AA contrast on all text (4.5:1 minimum)

## Animations
- Fade-in on scroll via IntersectionObserver — `opacity` + `transform` only (GPU)
- Duration: 0.5s ease-out
- Threshold: 0.08
- **Never animate** width, height, top, left — causes layout reflow

## Responsive Breakpoints
- **Desktop**: 680px max-width container, 2-column hero grid
- **≤640px**: single column, centered hero, full-width primary button
- **≤380px**: tighter padding (16px), smaller heading (34px)
- Nav links hidden on mobile, only nav CTA visible

## Photo Handling
The profile photo is embedded as `data:image/png;base64,...`
`object-position: 42% 28%` — centers the orange circle background with face.
Do not change object-position without visual check — it's been carefully tuned.

## CV Handling
CV PDF is embedded as base64 string in JS:
```js
const cvB64 = "...";
const cvBlob = new Uint8Array(atob(cvB64).split("").map(c => c.charCodeAt(0)));
const cvUrl = URL.createObjectURL(new Blob([cvBlob], {type: "application/pdf"}));
```
Do not remove or modify this — it enables offline CV download without a server.

## What to Improve (Design Focus)
- [ ] Add subtle entrance animations with stagger between hero elements
- [ ] Consider a dark mode variant using CSS `prefers-color-scheme`
- [ ] Service cards could have hover states (subtle lift or border color change)
- [ ] FAQ items could be expandable accordions to reduce scroll length
- [ ] Add a language toggle (SV/EN) — content currently Swedish only
- [ ] QR code could be generated and embedded directly on the page

## Anti-AI-Slop Rules (always follow)
- No Inter, Roboto, Arial or system fonts — DM Serif + DM Sans only
- No purple gradients on white
- SVG icons only — no emoji as UI elements
- `cursor: pointer` on ALL interactive elements
- Stable hover transitions — color/opacity/transform only, never layout shifts
- One primary CTA per section — no button soup
- Animate only `transform` and `opacity`

## Deployment
```bash
# Make changes to index.html
git add index.html
git commit -m "your message"
git push
# Live at cover.andreeabindar.se in ~60 seconds
```
