# AGENTS.md — Personal Branding Repo

## What this repo is

Personal branding hub for **Himath Rajapaksha** — a static portfolio site
(GitHub Pages) plus resume binaries. No build system, no framework: one
self-contained `index.html` with inline CSS/JS.

## Brand facts (single source of truth)

- **Name:** Himath Rajapaksha (full: R M Himath Hansada Rajapaksha)
- **Title/tagline:** Application Security Engineer & Full-Stack Developer
- **Hero carousel titles:** "FullStack Security Developer", "DevSecOps Architect", "Application Security Engineer"
- **Location:** Colombo, Sri Lanka
- **Email:** himath.hr@gmail.com
- **Phone:** +94-772610027
- **Site:** https://himath.work/
- **GitHub:** https://github.com/Himath-Rajapaksha
- **LinkedIn:** https://www.linkedin.com/in/himath-rajapaksha/
- **Education:** BSc (Hons) Cyber Security & Digital Forensics, Kingston University (2026–2027); Pearson BTEC Level 5 HND Computing (Cyber Security), ESOFt Metro Campus — Distinction (2025–2026)
- **Focus:** AppSec, RBAC, PostgreSQL RLS, hardened APIs; open to remote/hybrid AppSec internships
- **Tooling stack (marquee):** TypeScript, React, Node.js, Next.js, Tauri, Python, Rust, C#, PostgreSQL, Docker, Git, WebRTC, AppSec, Redis, Linux, JavaScript

Keep these consistent across `index.html`, the JSON-LD `Person` block, OG/Twitter
meta, and the resume files. If one changes, update all.

## Layout

```
Himath-Rajapaksha/                  # working dir (not a git repo)
├── AGENTS.md                       # this file
├── R M Himath Hansada Rajapaksha - Rsesume 2026aug07.docx
├── R M Himath Hansada Rajapaksha - Rsesume 2026aug07.pdf
└── Himath-Rajapaksha.github.io/    # the actual git repo (GitHub Pages)
    ├── index.html                  # entire site (HTML + inline CSS/JS)
    ├── robots.txt
    ├── sitemap.xml
    └── assets/                     # portrait + project screenshots + SVG tiles
        ├── portrait.jpg            # hero (loading="eager")
        ├── MacTop.png              # single tracked casing (consolidated 2026-10-26)
        ├── Huddl.png, AFO.png, Cap.png
        └── devpad.svg, shipnotes.svg, whitespace.svg, smartcrm.svg, kickblast.svg, sadl.svg   # project placeholder tiles
```

The git repo is `Himath-Rajapaksha.github.io/` (remote: origin/main). Run git
commands with `-C` or `cd` into it.

## Tech stack

- Static HTML/CSS/JS only — no package.json, no bundler, no framework.
- Fonts: Clash Grotesk 500/600 (`--font-display`) + Inter 400/700/900 (`--font-body`), loaded from the Fontshare/Google Fonts CDNs with preconnects — no vendoring.
- Deployed via GitHub Pages (branch deploy, not Actions — see commit `23112fa`).
- Live URL: https://himath.work/

## Common tasks

- **Preview locally:** open `index.html` in a browser (or `python3 -m http.server` in the site dir).
- **Deploy:** commit + push to `main` of `Himath-Rajapaksha.github.io`; Pages rebuilds.
- **Update resume:** regenerate both `.docx` and `.pdf` (keep the `2026aug07`-style date suffix; note the existing "Rsesume" typo in filenames — decide whether to rename and update any links).
- **Add a project:** add screenshot to `assets/`, add an `<a class="project-card">` in the projects grid in `index.html`, and update alt text.
- **Update SEO:** edit the meta/JSON-LD in `<head>` of `index.html` and bump `sitemap.xml`'s `lastmod`; `robots.txt` is frozen — do not edit it.

## Conventions

- Single file: all markup, styles, and scripts live in `index.html`. Keep it that way unless there's a strong reason to split.
- Inline CSS uses the rajib-kabir token set in `:root` — colors (`--color-bg #F5F1EC`, `--color-ink #1E1A1C`, `--color-ink-soft #3B3B3B`, `--color-body #2C2D2F`, `--color-white`, `--color-surface`, `--hairline`, `--gradient-brand`, `--gradient-blush`), radii (`--radius-card 20px`, `--radius-field 16px`, `--radius-pill 60px`, `--radius-btn 10px`), spacing (`12/16/30/100/120px`), sizes (`--size-container 1120px`, `--size-frame 1280px`, `--size-header 51px`), `--duration-reveal 600ms`. Reuse tokens; don't hardcode colors.
- `--color-muted` and `--color-mist` are declared but deliberately NEVER consumed: `#7E8083` fails AA at body sizes and nothing in this build is a large-bold muted text. Keep them unused — the batteries assert zero `var()` uses.
- Animations (motion inventory): hero marquees (`.marquee-track` via `marqueeL/R`, 36 s/46 s, `aria-hidden`, decorative copy), tooling ticker (`.ticker-track`, 30 s, IntersectionObserver pauses it offscreen), scroll reveals (`.fi` → `.v` via IntersectionObserver threshold .15 with `.fi-d1..3` stagger, 600 ms), card hover recipe (img scale 1.1 + blur 7px; blush overlay fades in at rotate −6°, wired to hover AND `:focus-visible`). No sticky section headings — all `.section-head`s are plain flow. The header is absolute and intentionally non-sticky (scrolls away).
- `prefers-reduced-motion: reduce` rules must stay style-final: zero out animation/transition durations, reset `scroll-behavior` to `auto`, freeze marquee/ticker tracks, force `.fi` visible. The `<head>` `<noscript>` guard keeps reveals visible without JS — when touching motion, QA both (static checks cover them).
- CTA-only gradient: `--gradient-brand` appears only on `.btn--gradient` CTAs — exactly one per surface family (header, hero, contact). Gradient button labels are `var(--color-ink)`: white failed the ≥3:1 endpoint gate on `#FF7A38` (2.59:1 computed), so the ruled fallback switched labels to ink (see design-spec ruling); don't revert to white without re-measuring. Fixed short centered labels are safe (worst-case label band ≈5.0:1); any NEW longer or left-justified CTA label re-opens the G6 gate on the violet end (endpoint 4.29:1); the white label is dead (2.59:1 on #FF7A38) — don't revert without re-measuring.
- No drop shadows: depth comes from frosted translucency (`--color-surface` + `backdrop-filter`) and hairlines (`--hairline`); cards carry no `box-shadow` (batteries fail anything but `none`).
- Responsive breakpoints: `min-width:768px` (nav links appear), `min-width:1200px` (work masonry `612fr 410fr`, training 3-up), with mobile variants `max-width:767.98px` (section padding 80/64) and `max-width:640px` (footer stacks single-column).
- Images: `loading="lazy"` except the hero portrait (`loading="eager"`, `fetchpriority="high"`). Every `<img>` must carry BOTH `width` and `height` attributes — it's the no-layout-shift gate. Keep `alt` text descriptive. QA batteries must check every `<img>` width/height attribute against the real file's dimensions — the portrait attr-vs-file drift (1600×686 vs 1469×1071 inherited from the old build) was caught only manually.
- Git commits: short imperative subject, often `feat:`/`fix:`/`Update` (see log: `feat: add SEO meta tags…`, `Fix footer: …`, `Update portfolio: …`). Keep subjects concise.

## SEO / structured data — don't break these

- `<title>`, meta description/keywords, canonical URL, OG + Twitter cards, and the JSON-LD `Person` block in `<head>`.
- `sitemap.xml` (single URL, priority 1.0; bump `lastmod` when real content changes) and `robots.txt` — robots is frozen: do not modify it, ever.
- If the canonical/site URL changes, update all of the above plus `sameAs` links.

## Known issues / gotchas (fix when touching related code)

Status after the 2026-10-27 rajib-kabir restyle — the theme swapped the 2026-10-26
build's fonts/palette/radius/spacing/breakpoints/motion (see Conventions); the QA
sweep of that restyle is in the git log (gradient CTA label switched to ink for
contrast, ticker strip padding + aria-label casing fixed, footer tagline restored
to the full source title line). Keep this list live: add new findings here, don't
reopen the closed ones.

1. **RESOLVED (2026-10-26): duplicate `checked` on nav radios** — single `checked` remains on `#nav-home`; `#nav-work` has none. (The radio-nav pattern is gone entirely since the restyle; nav is plain anchors now.)
2. **RESOLVED (2026-10-26): duplicate `.btn` CSS** — consolidated into a single `.btn` rule in the design-system style block.
3. **RESOLVED (2026-10-26): orphan CSS fragment** near the old `.contact-info` rule — stray properties with no selector were removed.
4. **RESOLVED (2026-10-26): extra closing `</div>`** in the projects section — removed; markup balanced.
5. **RESOLVED (2026-10-26): undefined classes** — `.section-label` and `.section-desc` are styled; stale `.project-row` (and `.reverse`) references dropped.
6. **RESOLVED (2026-10-26): asset casing** — single tracked `assets/MacTop.png`; HTML and tree reference that one casing only.
7. **RESOLVED (2026-10-26): unstyled `section-label`/`section-desc` headings** — styled in the redesign (overlaps item 5).
8. **OPTIONAL TIDY (2026-10-27, final-review triage): redundant nested `aria-hidden="true"` span** on the card-overlay ↗ arrow (the parent `.card-overlay` is already `aria-hidden`) — cosmetic, zero AT effect; optional post-merge tidy (the same classification applies to the marquee row/track nesting).
9. **OPEN (2026-10-27, final-review triage): heading-level skip h2 → h4** in the education/training cards (inherited source semantics) — retagging the edu-card h4s to h3 is a sanctioned cheap follow-up (CSS already covers `.edu-item h3,h4` identically), but the training section's floating h3s must first get a deliberate heading-strategy decision; keep OPEN until then.
10. **OPEN (2026-10-27, owner's call): footer Navigation column is a plain `<div>`, not `<nav>`** — `<nav aria-label="Site">` is an owner-optional nicety; all links stay keyboard-reachable either way.
11. **RESOLVED (2026-10-27, final-fix wave): content edge-flush below 1200px** — 20px inline inset applied to `.container`, the hero portrait/text/CTA bundle (`.hero-stage > :not(.marquee-row)`), and `.footer-card` below 1200px (restored on desktop); the two hero `.marquee-row`s remain full-bleed; no vertical paddings or ≥1200px geometry changed.
12. **DECLINED (2026-10-27, owner preview): the measured cards-over-headings sticky layering** — the spec's `.section-head` sticky effect (cards riding over the section label + display h2) stranded crisp letter fragments in the work grid's bare 12px gaps for the entire section scroll; owner ruled it a glitch at preview (`Shipped systems…` text visibly "on bg"). All `.section-head` sticky rules removed; headings flow normally above their grids. Don't re-add `position:sticky` to `.section-head` without owner consent — the frosted card bodies blur what's behind them, but gaps never can.

## Do not

- Don't commit secrets, tokens, or `.env` files.
- Don't rename the site directory or break the `Himath-Rajapaksha.github.io` GitHub Pages naming.
- Don't change the canonical URL without updating sitemap + robots + JSON-LD.
- Don't add a build step or framework unless explicitly requested — this is intentionally a zero-dependency static site.
- Don't "fix" the resume filename typo (`Rsesume`) silently — confirm with the owner first, since external links may reference it.
