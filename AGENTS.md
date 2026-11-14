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
- **Tooling stack (marquee):** TypeScript, React, Node.js, Next.js, Tauri, Python, Rust, C#, PostgreSQL, Docker, Git, WebRTC, AppSec, Redis, Linux, JavaScript, eBPF, CI/CD

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
    ├── favicon.ico + favicon-16x16.png + favicon-32x32.png + apple-touch-icon.png + android-chrome-192x192.png + android-chrome-512x512.png + site.webmanifest   # favicon set unwrapped from favicon_io.zip (2026-10-27); keep at ROOT
    └── assets/                     # portrait + project tile images (screenshots + mock tiles)
        ├── portrait.jpg            # hero (1469×1071, loading="eager")
        ├── MacTop.png              # single tracked casing
        ├── Huddl.png, AFO.png, Cap.png
        ├── devpad.png, shipnotes.png, whitespace.png, smartcrm.png, kickblast.png, sadl.png, 3y3.png   # regenerated 2026-10-27 replacing the six SVG placeholder tiles — 3 live screenshots + 4 Apple-style mock tiles
        ├── founder-skill.png, bytesmith.png, prompt-vault.png   # 2026-11-02 skills+prompts batch — 2 mocks (founder-skill, prompt-vault) + 1 live hero capture (bytesmith), all 1672×941
        └── og-cover.png            # 2026-11-14 social preview card (1200×630) — the og:image / twitter:image target, type-led with the hero portrait on the right
```

The git repo is `Himath-Rajapaksha.github.io/` (remote: origin/main). The
owner pushes manually — never push. Local main was merged with origin/main
(2026-10-27), so `git push origin main` fast-forwards whenever the owner
chooses to publish.

## Tech stack

- Static HTML/CSS/JS only — no package.json, no bundler, no framework.
- Fonts: Inter (300–700) for everything + **Space Grotesk 600** for the hero accent phrase only — one Google Fonts request, preconnects, no vendoring. Owner approved the second family on 2026-11-14 for the scramble; don't add a third.
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
- **Hero title rotator = character scramble (2026-11-14)**: `.flip-wrap` is an `inline-grid` of three stacked `.flip-word` spans — only `.is-active` is `visibility:visible`, the others keep their width so the block never resizes — plus a `.sr-only` `aria-live="polite"` line (`#flipSr`) that carries the announcement (the visual words are `aria-hidden`). Every 3.7 s the visible word jumbles out (~190 ms) and the next decodes left→right (~760 ms). Each character is a `.ch` box whose width is frozen to the real glyph advance (`getBoundingClientRect` before the glyph swap), so random glyphs cannot reflow the line; a `setTimeout` fallback settles the word if rAF is throttled, and reduced motion swaps instantly. Accent face: Space Grotesk 600, `letter-spacing:-0.032em`.
- Reveal system: `.fi` (opacity 0 + translateY(20px), 0.7 s) gains `.v` via IntersectionObserver (threshold 0.12, rootMargin bottom −30px, unobserve after reveal); stagger classes `.fi-d1..d5` (0.1–0.5 s); no-IO fallback adds `.v` to everything. The `<head>` `<noscript>` guard (`.fi { opacity:1 !important; transform:none !important }`) keeps content visible without JS — keep it after the font link, before the `<style>`.
- Tools marquee: one `.marquee-track` row, 16-item list duplicated 2×, `@keyframes marquee-scroll` translateX 0→−50%. Animated by CSS only (no JS pause). (Now 18 chips ×2 after 2026-10-27; halves byte-identical — keep it that way.)
- **DevTools easter egg (2026-10-27):** the trailing `<script>` block logs a `%c`-styled console banner on load and exposes `window.himath` (`whoami`, `contact`, `version`) — console-only, zero page visuals. Owner-approved; don't strip it in cleanup passes.
- Projects: `.projects-grid` is a hard 2-col grid (`1fr 1fr`, gap 4px, radius 0), mobile → 1fr at 768px; cards are plain `<a>` with `<img>` (no overlays, no blur/scale hover recipe in this design).
- **Project-tile glass hover (2026-11-14, owner-chosen "V1 sheet"):** every `.project-card` carries `style="--img:url('assets/X.png')"` plus an `aria-hidden` overlay — `<span class="pc-glass">` holding `.pc-frost` and `.pc-body` (`.pc-title`, `.pc-meta`, `.pc-cta` as a `<span>`, **never** a nested `<a>`, so the whole card stays one link). At rest `.pc-glass` sits at `translateY(101%)` and rises in 440 ms `cubic-bezier(.22,1,.36,1)`; title/meta/cta fade + rise on a 70/110/170 ms stagger (340/340/300 ms), the `<img>` eases to `scale(1.02)`, and two 1px masked borders fade in (`::before` white radial from the top-left corner, `::after` accent radial from the bottom-right — radial, not `135deg/315deg`, or the accent paints a red hairline down the whole right edge). Exit is 240 ms, un-staggered. `.pc-frost::before` is a **blurred duplicate of the tile** (`background-image:var(--img)`, `blur(32px) saturate(1.15)`, `scale(1.08)`), masked so the top of the screenshot stays sharp — do **not** swap it for `backdrop-filter`: a mask on the same element makes it a backdrop root in Chrome and the blur silently stops rendering. Touch (`hover:none`) hides the overlay entirely, `:focus-visible` shows the settled state, and `prefers-reduced-motion` collapses it to an instant swap. Rest state is pixel-identical to the pre-change page (verified by diffing full-page captures).
- Contact: `contact-heading` (with `<em>` on "Drop me a line.") + two plain buttons `.btn-dark` (Email) and `.btn-light` (LinkedIn). Footer is a single copyright line.
- Breakpoints: `max-width:900px` (dead `.project-row` rules — see Known issues), `768px` (headline 26px, flip-wrap block, tighter `.btn`, projects-grid → 1fr @ :519), `640px` (hero padding; a redundant second `.projects-grid` 1fr rule @ :721).
- `prefers-reduced-motion: reduce` freezes `.eyebrow-dot` + `.btn` transitions and makes the hero rotator swap words instantly (JS-level, live-updated through `matchMedia`). It does NOT zero `.fi` reveals — extending coverage is a sanctioned nicety (see Known issues).
- Images: `loading="lazy"` except the hero portrait (`loading="eager"`). The portrait carries real-dimension attrs (`width="1469" height="1071"`) paired with `height: auto` on `.hero-portrait` — any new width/height attr must pair with `height:auto` or the height hint locks and distorts. Card `<img>`s currently have NO attrs (deployed parity; see Known issues). Keep `alt` text descriptive.
- **Favicons live at repo ROOT, not assets/** (`favicon.ico` auto-discovery + `<head>` link tags + `site.webmanifest` with name/short_name from brand facts). Don't move them into assets/ unless re-wiring the links in the same change.
- **Dead CSS (render-none — don't activate):** `.hero-portrait img` + `.hero-portrait:hover img` (grayscale/hover targets a child `<img>` that doesn't exist; the portrait renders in COLOR and hover does nothing), `.project-row`/`.project-row.reverse` (no such elements), `.contact-info` (unreferenced). Re-aiming or deleting them changes/postpones visuals — owner's call.
- Git commits: short imperative subject, often `feat:`/`fix:`/`Update`. Keep subjects concise.

## SEO / structured data — don't break these

- `<title>`, meta description/keywords, canonical URL, OG + Twitter cards, and the JSON-LD `Person` block in `<head>`.
- **`<title>` is just `Himath.work`** (2026-10-27, owner directive — clean browser tab). The descriptive tagline stays in og:title / twitter:title / JSON-LD `name` / meta description — don't re-expand `<title>` without owner direction.
- **Social preview:** `og:image` + `twitter:image` both point at `assets/og-cover.png` (1200×630, 1.91:1, ~250 KB, owner-picked design 2026-11-14) with `og:image:width/height/type/alt` and `twitter:image:alt` alongside; `twitter:card` stays `summary_large_image`. The card is a composed layout — 96 px left margin, kicker / name / accent role / subtitle / `himath.work`, portrait bleeding to the right edge (panel starts at 800 px, `background-position:54%`) — not a page screenshot. Regenerating it means re-rendering the card at exactly 1200×630 with the site's Inter + Space Grotesk and re-exporting to the same path, because chat clients cache the old scrape: WhatsApp, X and Facebook only refetch when the image URL changes or the scraper is re-run.
- **Canonical URL = `https://himath.work/` everywhere** in index.html (canonical, og:url, og:image, twitter:image, JSON-LD `url`/`image`) and in `sitemap.xml` (`lastmod 2026-11-14`). The old-domain himath-rajapaksha.github.io refs were migrated to himath.work by the owner's `7dd1ba2`; the 2026-10-27 restore preserved those URL strings.
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
12. **RESOLVED (2026-10-27): 11-card odd grid** — 3y3 moved to the closing row and spanned full-width via `.project-card.full { grid-column: 1 / -1; }`: the grid now ends in five full rows plus one full-width quiet closer — no empty cell. If cards are added or removed later, re-check parity (even counts keep the tight grid; an odd count needs a spanning closer).
13. **RESOLVED (2026-11-02): 14-card grid (skills+prompts batch)** — founder-skill + bytesmith added as a pair row after ShipNotes, prompt-vault added **full-width** before 3y3. Grid = six pair-rows + two full-width rows (12 regular + 2 full), no empty cell. Tile sources: `founder-skill.html`/`prompt-vault.html` mocks + Round-3 CSS in `mocks-apple/`, rendered by `render3.sh` (canonical flags, md5 determinism, `qa3.js` bleed-aware QA); `bytesmith.png` is a live capture of bytesmith-rust.vercel.app. Rule intact: mocks bleed by design (founder-skill card → right edge; prompt-vault chips → both edges) while prose never touches the tile margins.

14. **RESOLVED (2026-11-14): hero accent overflowed sideways at 769–1100 px** — `white-space:nowrap` on `.flip-word` let the longest title (`Application Security Engineer`, 1007 px at 72 px Inter) exceed the viewport: 1051 px of content at a 900 px window, i.e. a horizontal scrollbar and a clipped accent line. `.flip-word` is now `white-space:normal`, so the phrase wraps when it cannot fit; it still sits on one line at ≥1150 px and at ≤768 px. Verified: `scrollWidth ≤ innerWidth` at 500/720/780/900/1024/1280.

15. **BY DESIGN (2026-11-14): the glass overlay repeats text baked into the tile** — MacTop, AFO, Cap, Smart CRM and friends already carry their own headline in the screenshot, so a hover shows that headline above the frost and the overlay's `.pc-title` below it. That is intended: the overlay is the tile's label plus its destination URL, and it is the only place a project's name/URL appears in this design (the alt text is for AT only). Don't "solve" it by hiding the title or by editing the tile art without owner direction.

## Do not

- Don't push to origin — **the owner pushes manually.**
- Don't commit secrets, tokens, or `.env` files.
- Don't rename the site directory or break the `Himath-Rajapaksha.github.io` GitHub Pages naming.
- Don't change the canonical URL without updating sitemap + JSON-LD + meta (robots.txt stays frozen).
- Don't add a build step or framework unless explicitly requested — this is intentionally a zero-dependency static site.
- Don't re-theme (Quartz/rajib-kabir or otherwise) — the deployed look is the owner-approved design; 2026-10-27's restyle was rejected at preview.
- Don't "fix" the resume filename typo (`Rsesume`) silently — confirm with the owner first, since external links may reference it.
