# himath.work

Source for **[himath.work](https://himath.work/)** — a single-page portfolio for
Himath Rajapaksha, plus the resume binaries.

Static site: one self-contained `index.html` with inline CSS and JavaScript.
No build step, no framework, no dependencies.

## Structure

| path | contents |
| --- | --- |
| `index.html` | the entire page — markup, styles and scripts |
| `CNAME` | custom domain (`himath.work`) |
| `sitemap.xml`, `robots.txt` | crawler config |
| `site.webmanifest` | PWA manifest (name, icons, theme) |
| `favicon.ico`, `favicon-16x16.png`, `favicon-32x32.png`, `apple-touch-icon.png`, `android-chrome-*.png` | icon set (kept at root for autodiscovery) |
| `assets/` | portrait and project tile images |

## Preview locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy

Deployed with GitHub Pages from `main`. Push and Pages rebuilds — there is no CI
step and no generated output committed.

## Editing notes

- Reuse the CSS custom properties in `:root` (`--bg`, `--text`, `--accent`,
  `--muted`, `--border`, `--card-bg`, `--sans`) instead of hardcoding colours.
- SEO lives in `<head>`: title, description, canonical, Open Graph, Twitter card,
  and the JSON-LD `Person` block. If the canonical URL changes, update the
  sitemap and the JSON-LD `url`/`image` with it.
- Project cards are plain `<a>` elements with a screenshot; the grid is a hard
  two-column layout that collapses to one column on mobile.
