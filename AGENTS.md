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
    └── assets/                     # portrait.jpg + project screenshots
        ├── portrait.jpg
        ├── Mactop.png, MacTop.png  # note: two casings exist — keep both or clean up
        ├── Huddl.png, AFO.png, Cap.png
```

The git repo is `Himath-Rajapaksha.github.io/` (remote: origin/main). Run git
commands with `-C` or `cd` into it.

## Tech stack

- Static HTML/CSS/JS only — no package.json, no bundler, no framework.
- Deployed via GitHub Pages (branch deploy, not Actions — see commit `23112fa`).
- Live URL: https://himath.work/

## Common tasks

- **Preview locally:** open `index.html` in a browser (or `python3 -m http.server` in the site dir).
- **Deploy:** commit + push to `main` of `Himath-Rajapaksha.github.io`; Pages rebuilds.
- **Update resume:** regenerate both `.docx` and `.pdf` (keep the `2026aug07`-style date suffix; note the existing "Rsesume" typo in filenames — decide whether to rename and update any links).
- **Add a project:** add screenshot to `assets/`, add an `<a class="project-card">` in the projects grid in `index.html`, and update alt text.
- **Update SEO:** edit the meta/JSON-LD in `<head>` of `index.html`, plus `sitemap.xml` (`lastmod`) and `robots.txt`.

## Conventions

- Single file: all markup, styles, and scripts live in `index.html`. Keep it that way unless there's a strong reason to split.
- Inline CSS uses CSS variables in `:root` (`--bg`, `--text`, `--accent #E85D4A`, `--muted`, `--border`, `--sans` Inter). Reuse variables; don't hardcode colors.
- Animations: `.fi` + `.fi-dN` fade-in classes driven by IntersectionObserver; `.flip-track` word rotation. Respect `prefers-reduced-motion`.
- Responsive breakpoints: 900px, 768px, 640px.
- Images: `loading="lazy"` except the hero portrait (`loading="eager"`). Keep `alt` text descriptive.
- Git commits: short imperative subject, often `feat:`/`fix:`/`Update` (see log: `feat: add SEO meta tags…`, `Fix footer: …`, `Update portfolio: …`). Keep subjects concise.

## SEO / structured data — don't break these

- `<title>`, meta description/keywords, canonical URL, OG + Twitter cards, and the JSON-LD `Person` block in `<head>`.
- `robots.txt` and `sitemap.xml` (single URL, priority 1.0).
- If the canonical/site URL changes, update all of the above plus `sameAs` links.

## Known issues / gotchas (fix when touching related code)

1. **Duplicate `checked` on nav radios** — both `#nav-home` and `#nav-work` carry `checked`; only the last wins. Remove `checked` from `#nav-work`.
2. **Duplicate `.btn` CSS** — defined once in the hero block (padding 13px 24px, radius 10px) and again in the contact block (0.85rem 1.8rem, radius 10px). Consolidate.
3. **Orphan CSS fragment** around the `.contact-info` rule (lines ~622–624): stray `outline: none; transition: …; }` with no selector. Remove.
4. **Extra closing `</div>`** in the projects section (after the grid). Remove to keep DOM balanced.
5. **Undefined classes** referenced in markup but not styled: `.section-label`, `.section-desc`, `.project-row` (and its `.reverse`). Either style them or drop the references.
6. **Two asset casings:** `Mactop.png` and `MacTop.png` both exist; HTML references `Mactop.png`. Consolidate to one file to avoid case-sensitivity bugs on Linux/Pages.
7. **No `section-label`/`section-desc` styles** — headings render unstyled.

## Do not

- Don't commit secrets, tokens, or `.env` files.
- Don't rename the site directory or break the `Himath-Rajapaksha.github.io` GitHub Pages naming.
- Don't change the canonical URL without updating sitemap + robots + JSON-LD.
- Don't add a build step or framework unless explicitly requested — this is intentionally a zero-dependency static site.
- Don't "fix" the resume filename typo (`Rsesume`) silently — confirm with the owner first, since external links may reference it.
