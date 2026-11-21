# AGENTS.md

## What this is
Single-page static portfolio (Indonesian copy, `lang="id"`). No build step, package manager, dependencies, tests, lint, or CI. Entrypoint: `index.html`; all styling in `css/style.css`; all JS in `js/script.js`.

## Run and verify
- Open `index.html` directly in a browser, or serve via Laragon at `http://localhost/portfolio_latihan-main/portfolio_latihan-main/`.
- Internet is required: Tailwind Play CDN, GSAP 3.12.5, and ScrollTrigger load from CDNs.
- No automated checks exist. Verify manually: loader disappears and page scrolls; hero/about/project reveals fire; layout at ~1280px, <=800px, <=540px, and 320px (README task 11); OS reduced-motion setting disables animation.

## Styling gotchas
- Styling is vanilla CSS with custom properties, not Tailwind utilities. The only Tailwind use is the inline `tailwind.config` in `index.html` plus `bg-paper text-ink antialiased` on `<body>`.
- Palette is duplicated: `paper`/`ink`/`moss`/`clay` exist in both the inline Tailwind config (`index.html`) and `:root` in `style.css`. Change both.
- Naming is BEM-like (`block__element--modifier`); follow it for new components. Responsive breakpoints are 800px and 540px; page width is `min(100% - 96px, 1248px)` via `.page-wrap`/`.section-wrap`.
- The arrow SVG is inlined at every link; update all copies when changing it.

## JS gotchas
- `body.is-loading` sets `overflow: hidden`; the loader overlay covers the page. `finishLoading()` is the fallback when the loader is missing, GSAP is unavailable, or reduced motion is on. Preserve that fallback or the page becomes unscrollable.
- Reduced motion is intentionally handled in both JS (`prefersReducedMotion`) and CSS (`@media (prefers-reduced-motion: reduce)`). README requires animations stay comfortable with it enabled.
- `script.js` expects GSAP/ScrollTrigger globals from the CDN scripts that precede it in `index.html`; keep script order.

## Content rules
- Do not invent facts, numbers, links, or project details. Copy comes from the facilitator; the email `halo@fahdin.dev` and social URLs are known placeholders (README tasks 1-2, 9).
- Keep user-facing copy in Indonesian. Follow README's contribution rules (one task per PR, mobile + desktop check, ask before adding dependencies or changing design direction).

## Git workflow
- This directory is **not a git repo yet** (no `.git`).
- `github-guide-global.md` is the authoritative Git SOP: mandatory Session Setup before any branch/commit/PR, one PR per session then hard stop, commit/PR formats per chosen style, and forbidden destructive commands. Read it before any git action.
- `semantic-versioning-guide.md` summarizes SemVer; where they conflict, `github-guide-global.md` wins.
