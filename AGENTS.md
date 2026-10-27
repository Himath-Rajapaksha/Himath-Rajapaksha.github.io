# AGENTS.md — Personal Branding Repo

> Note: mirrored to `/home/anorak/Himath-Rajapaksha/AGENTS.md` (working dir copy
> without the git repo). Update both when this file changes.

## What this repo is

Personal branding hub for **Himath Rajapaksha** — a static portfolio site
(GitHub Pages) plus resume binaries. No build system, no framework: one
self-contained `index.html` with inline CSS/JS.

**Design authority: the deployed himath.work build.** Its index.html bytes are
`19dc66e` on origin/main; the owner's own migration commit `7dd1ba2` ("feat:
serve site on custom domain himath.work", in local history) already carried
CNAME/robots/sitemap and the six index.html URLs to himath.work. On 2026-10-27
the owner rejected the rajib-kabir restyle at preview ("design is not the same
as i thought — major issues") and `index.html` was restored to the deployed
design: origin's index bytes re-based with `7dd1ba2`'s URL migration preserved
and only sanctioned invisible fixes on top — `git diff 7dd1ba2 HEAD --
index.html` shows exactly those. Restyle history `824531a..7e66d19` is kept as
rejected reference; do not re-theme or restyle without explicit owner direction.

## Brand facts (single source of truth)

- **Name:** Himath Rajapaksha (full: R M Himath Hansada Rajapaksha)
- **Title/tagline:** Application Security Engineer & Full-Stack Developer
- **Hero flip-track titles:** "FullStack Security Developer", "DevSecOps Architect", "Application Security Engineer"
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
├── AGENTS.md                       # mirror of this file
├── R M Himath Hansada Rajapaksha - Rsesume 2026aug07.docx
├── R M Himath Hansada Rajapaksha - Rsesume 2026aug07.pdf
└── Himath-Rajapaksha.github.io/    # the actual git repo (GitHub Pages)
    ├── index.html                  # entire site (HTML + inline CSS/JS)
    ├── CNAME                       # himath.work (GitHub Pages custom domain)
    ├── robots.txt                  # FROZEN — never edit
    ├── sitemap.xml
    └── assets/                     # portrait + project tile images (screenshots + mock tiles)
        ├── portrait.jpg            # hero (1469×1071, loading="eager")
        ├── MacTop.png              # single tracked casing
        ├── Huddl.png, AFO.png, Cap.png
        └── devpad.png, shipnotes.png, whitespace.png, smartcrm.png, kickblast.png, sadl.png, 3y3.png   # regenerated 2026-10-27 replacing the six SVG placeholder tiles — 3 live screenshots + 4 Apple-style mock tiles
```

The git repo is `Himath-Rajapaksha.github.io/` (remote: origin/main). The
owner pushes manually — never push. Local main was merged with origin/main
(2026-10-27), so `git push origin main` fast-forwards whenever the owner
chooses to publish.

## Tech stack

- Static HTML/CSS/JS only — no package.json, no bundler, no framework.
- Font: Inter (300–700) from Google Fonts CDN with preconnects — no vendoring, no second family.
- Deployed via GitHub Pages (branch deploy, not Actions).
- Live URL: https://himath.work/

## Common tasks

- **Preview locally:** open `index.html` in a browser (or `python3 -m http.server` in the site dir).
- **Deploy:** owner commits + pushes to `main` of `Himath-Rajapaksha.github.io`; Pages rebuilds. Do not push on the owner's behalf.
- **Update resume:** regenerate both `.docx` and `.pdf` (keep the `2026aug07`-style date suffix; note the existing "Rsesume" typo in filenames — decide whether to rename and update any links).
- **Add a project:** add screenshot to `assets/`, add an `<a class="project-card">` in `projects-grid`, and update alt text.
- **Update SEO:** edit the meta/JSON-LD in `<head>` of `index.html` and bump `sitemap.xml`'s `lastmod`; `robots.txt` is frozen — do not edit it.

## Conventions

- Single file: all markup, styles, and scripts live in `index.html`. Keep it that way unless there's a strong reason to split.
- Inline CSS uses the deployed token set in `:root` — `--bg #FFFFFF`, `--text #1A1A1A`, `--accent #E85D4A`, `--muted #6B6B6B`, `--border #E8E6E1`, `--card-bg #FFFFFF`, `--sans` Inter. Reuse tokens; don't hardcode colors. Accent use is sparing (active nav label, flip words, eyebrow dot, hover accents).
- **Nav = CIR-TABS radio pattern** (fixed top-center): three hidden radios `name="nav"` (`#nav-home` carries the single `checked`) + styled labels; scroll-spy JS checks the active radio from `scrollY + innerHeight/3` and forces the last index near page bottom; label clicks `scrollIntoView` smooth with an 800 ms scroll-lock. Don't add a second `checked` attribute — one only (HTML spec resolves dup:checked against the LAST one).
- **Hero flip-track rotator**: `.flip-wrap` (overflow hidden, 1.2em) + `#flipTrack` flex column stepped via `translateY(-idx * wordHeight)` every 3.7 s; word list duplicated in markup for the wrap; JS measures `.flip-word` offsetHeight. Keep `aria-live="polite"` + the `aria-label` on the wrapper.
- Reveal system: `.fi` (opacity 0 + translateY(20px), 0.7 s) gains `.v` via IntersectionObserver (threshold 0.12, rootMargin bottom −30px, unobserve after reveal); stagger classes `.fi-d1..d5` (0.1–0.5 s); no-IO fallback adds `.v` to everything. The `<head>` `<noscript>` guard (`.fi { opacity:1 !important; transform:none !important }`) keeps content visible without JS — keep it after the font link, before the `<style>`.
- Tools marquee: one `.marquee-track` row, 16-item list duplicated 2×, `@keyframes marquee-scroll` translateX 0→−50%. Animated by CSS only (no JS pause).
- Projects: `.projects-grid` is a hard 2-col grid (`1fr 1fr`, gap 4px, radius 0), mobile → 1fr at 768px; cards are plain `<a>` with `<img>` (no overlays, no blur/scale hover recipe in this design).
- Contact: `contact-heading` (with `<em>` on "Drop me a line.") + two plain buttons `.btn-dark` (Email) and `.btn-light` (LinkedIn). Footer is a single copyright line.
- Breakpoints: `max-width:900px` (dead `.project-row` rules — see Known issues), `768px` (headline 26px, flip-wrap block, tighter `.btn`, projects-grid → 1fr @ :519), `640px` (hero padding; a redundant second `.projects-grid` 1fr rule @ :721).
- `prefers-reduced-motion: reduce` freezes `.flip-track`, `.eyebrow-dot`, and `.btn` transitions only (style-final). It does NOT zero `.fi` reveals — extending coverage is a sanctioned nicety (see Known issues).
- Images: `loading="lazy"` except the hero portrait (`loading="eager"`). The portrait carries real-dimension attrs (`width="1469" height="1071"`) paired with `height: auto` on `.hero-portrait` — any new width/height attr must pair with `height:auto` or the height hint locks and distorts. Card `<img>`s currently have NO attrs (deployed parity; see Known issues). Keep `alt` text descriptive.
- **Dead CSS (render-none — don't activate):** `.hero-portrait img` + `.hero-portrait:hover img` (grayscale/hover targets a child `<img>` that doesn't exist; the portrait renders in COLOR and hover does nothing), `.project-row`/`.project-row.reverse` (no such elements), `.contact-info` (unreferenced). Re-aiming or deleting them changes/postpones visuals — owner's call.
- Git commits: short imperative subject, often `feat:`/`fix:`/`Update`. Keep subjects concise.

## SEO / structured data — don't break these

- `<title>`, meta description/keywords, canonical URL, OG + Twitter cards, and the JSON-LD `Person` block in `<head>`.
- **Canonical URL = `https://himath.work/` everywhere** in index.html (canonical, og:url, og:image, twitter:image, JSON-LD `url`/`image`) and in `sitemap.xml` (`lastmod 2026-10-27`). The old-domain himath-rajapaksha.github.io refs were migrated to himath.work by the owner's `7dd1ba2`; the 2026-10-27 restore preserved those URL strings.
- `robots.txt` is FROZEN: locally it already reads `Sitemap: https://himath.work/sitemap.xml` (the owner's `7dd1ba2` migration; publishes on the next push), while origin's copy still shows the old domain, which resolves via the Pages redirect in the meantime. Do not modify robots.txt.
- If the canonical/site URL changes, update all of the above plus `sameAs` links.

## Known issues / gotchas (fix when touching related code)

Status after the 2026-10-27 restore to the deployed himath.work design. The
restore deliberately re-imported some deployed code debt (it was only ever
cleaned in the unpushed restyle builds). Keep this list live: add new findings
here, don't reopen the closed ones.

1. **RESOLVED (2026-10-27, restore): duplicate `checked` on nav radios** — single `checked` on `#nav-home`; `#nav-work`/`#nav-contact` carry none. (Spec resolves dup:checked to the LAST member, so the deployed build's no-JS first paint briefly showed "Work" active; scroll-spy sets the radio on load for everyone else — effectively zero delta.)
2. **OPEN (deployed debt, inert): duplicate `.btn` rules** (~:294 px-based, ~:586 rem-based) — the later rem rule wins by cascade; consolidation must keep the later values, or nothing changes visually.
3. **OPEN (deployed debt, inert): orphan CSS fragment** right after `.contact-info` — selectorless `outline`/`transition` declarations with a dangling `}`; browser-parsed as junk, zero effect. Remove only with the `.contact-info` dead-rule decision.
4. **RESOLVED (2026-10-27, restore): stray extra `</div>`** in the projects section (after the grid close) — removed; markup balanced.
5. **OPEN (deployed debt): dead selectors** `.hero-portrait img`/`.hero-portrait:hover img` (grayscale hover never fires — portrait is color), `.project-row`/`.project-row.reverse`, `.contact-info`. Deleting = invisible; RE-AIMING any of them = a visual change needing owner approval.
6. **OPEN (deployed debt): `.section-label`/`.section-desc` unstyled** — "Selected Work" heading renders as a default-weight h2/p (deployed look). Styling them = visual change, owner's call.
7. **RESOLVED (2026-10-27, restore + merge): asset casing** — tree + HTML both reference `assets/MacTop.png` (origin's dual-case blobs were consolidated to the single `MacTop.png` by the local rename, and the restore re-cased the HTML ref; on case-sensitive Pages either side alone would have 404'd the card image).
8. **OPEN (CLS nicety): card imgs lack width/height attrs** (`MacTop.png` 1672×941, Huddl/AFO/Cap too) — below-fold lazy images, deployed parity. Adding attrs requires the `height:auto`-paired pattern (see Conventions).
9. **OPEN (a11y nicety): prefers-reduced-motion doesn't cover `.fi` reveals** — extending the frozen set is sanctioned; don't shoehorn other motion changes at the same time.
10. **LOCKED: robots.txt** — locally reads `Sitemap: https://himath.work/sitemap.xml` (owner's `7dd1ba2` migration; publishes on push). Never edit robots.txt; treat as correct-by-construction.
11. **HISTORY NOTE: the rajib-kabir restyle (commits `824531a..7e66d19`) is rejected design history** — its extra sections (training, education, frosted cards, sticky section heads, ticker, footer nav) do NOT exist in this design. mined for content only, never for style, without owner direction.

## Do not

- Don't push to origin — **the owner pushes manually.**
- Don't commit secrets, tokens, or `.env` files.
- Don't rename the site directory or break the `Himath-Rajapaksha.github.io` GitHub Pages naming.
- Don't change the canonical URL without updating sitemap + JSON-LD + meta (robots.txt stays frozen).
- Don't add a build step or framework unless explicitly requested — this is intentionally a zero-dependency static site.
- Don't re-theme (Quartz/rajib-kabir or otherwise) — the deployed look is the owner-approved design; 2026-10-27's restyle was rejected at preview.
- Don't "fix" the resume filename typo (`Rsesume`) silently — confirm with the owner first, since external links may reference it.
