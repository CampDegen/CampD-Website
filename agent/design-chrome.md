# Design chrome (homepage vs pack)

Stable UI rules. Pack **source** is CampD-SPT-Pack; this repo only mirrors `spt-pack/` after sync.

## Token source of truth

| Doc | Use |
|---|---|
| [`colors.md`](../colors.md) | Semantic token **names** and palette intent |
| [`css/styles.css`](../css/styles.css) | **Live aged hex** on campdegen.com (slightly warmed vs the table in `colors.md`) |

When pack `css/themes/facility.css` drifts, copy `:root` and body background/grain/vignette from `css/styles.css`. Do not `@import` the homepage stylesheet into the pack — class names differ (`.site-nav` vs `.pack-nav`, catalog components).

## Homepage (`/`)

- Edit: `index.html`, `css/styles.css` in **this repo**.
- `.site-header`: **`position: sticky`** — masthead stays at top while scrolling.
- Primary nav in header: Overview (`#about`), SPT Pack (`/spt-pack/`), Communications (`#connect`).
- One Safety Orange CTA per viewport (Discord on hero).
- Fonts: Bebas Neue (headings), Rajdhani (body), Share Tech Mono (labels/nav/meta).
- `font-size: 1.125rem` on **`body` only** (not `html`) so `rem` units match browser default root.

## SPT pack (`/spt-pack/`)

- Edit: **CampD-SPT-Pack** repo (`css/themes/facility.css`, `index.html`, `settings.html`, `looking.html`). Never hand-edit `spt-pack/` here.
- Masthead matches homepage **look** (logo, CampD wordmark, double border, dashed `header-meta` doc strip) but:
  - **No** Overview / SPT Pack / Communications tabs in the masthead.
  - `.site-header`: **`position: relative`** — scrolls away with the page (subpages only; homepage stays sticky).
- Pack section nav: `.pack-nav` below header — Mods, Pack Settings, Looking to add (same button styling as `.site-nav a`).
- Brand link → `https://campdegen.com/`.
- SPT version in `header-meta` doc strip (`#spt-chip`, filled from `data/site.json`).
- Favicon: same PNG as homepage (`assets/favicon.png` in pack assets).
- Skip link + `main#main-content` on pack pages.
- No second Safety Orange button on pack pages; hazard tape on hero is OK.

## rem / scale pitfall

If pack CSS sets `font-size: 1.125rem` on **`html`**, every `rem` (logo `2.5rem`, brand `1.75rem`, `--header-height`) scales ~12.5% larger than the homepage. Match homepage: size on **`body` only**.

## Publish pack UI changes

1. Push CampD-SPT-Pack `main` (Loneranger419).
2. Run **Sync SPT Pack** on this repo (or wait 06:30 UTC cron).
3. Verify `https://campdegen.com/spt-pack/`.

Staging-only preview: pack repo root or github.io project Pages — relative asset URLs must stay relative.

## Pack chrome still open (edit pack repo)

- OG/Twitter meta on pack pages.
- Footer closer to homepage `.site-footer`.
- Optional: shared footer block copy.

See pack repo `SPT_MERGE_KNOWLEDGE.md` for catalog/Forge rules.
