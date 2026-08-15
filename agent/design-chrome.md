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
- Primary nav in header: Overview (`#about`), Communications (`#connect`). SPT Pack lives on the hero **clipboard index** (`aside.clipboard` → `/spt-pack/`), not as a header button.
- Clipboard uses a US Letter `8.5 / 11` aspect ratio. Its exposed board is dark, oil-worn wood/hardboard with steel clip hardware; the paper contains boxed shortcut links.
- One Safety Orange CTA per viewport (Discord on hero).
- Fonts: Bebas Neue (headings), Rajdhani (body), Share Tech Mono (labels/nav/meta).
- `font-size: 1.125rem` on **`body` only** (not `html`) so `rem` units match browser default root.
- Aging overlays: real `.film-grain` / `.vignette` nodes + `assets/grain.png`. Do **not** use SVG `feTurbulence` data-URI backgrounds — Chromium often skips them on first paint (cooler/bluer page until refresh).

## Homepage clipboard index

The clipboard is a homepage-only component. Recreate it with this DOM shape inside `.hero-briefing`, after `.hero-content`:

```html
<aside class="clipboard" aria-labelledby="index-heading">
  <div class="clipboard-board">
    <span class="clipboard-clip" aria-hidden="true"></span>
    <div class="clipboard-paper">
      <!-- document metadata + heading -->
      <ol class="clipboard-list">
        <li>
          <a href="/spt-pack/">
            <span class="clipboard-link-title">SPT Pack</span>
            <span class="clipboard-link-detail">Mod catalog</span>
          </a>
        </li>
      </ol>
    </div>
  </div>
</aside>
```

Add later shortcuts as additional `<li>` elements using the same link-title/link-detail structure.

CSS constraints that matter:

- At `64rem+`, `.hero-briefing` has three columns: `11rem minmax(0, 1fr) minmax(19rem, 20.75rem)`. The third child is the clipboard.
- `.hero-emblem` must remain `align-self: start`; otherwise a stretched grid row moves the logo down.
- `.clipboard` uses `aspect-ratio: 8.5 / 11`. Its desktop override (`width: 100%; height: auto; align-self: start`) must appear **after** the base `.clipboard` rule or the cascade will produce a narrow 1:2 board.
- Do not set clipboard `height: 100%`. Width determines the Letter ratio; the resulting grid row lets the briefing card reach a similar height.
- Below `64rem`, the clipboard stacks and centers at a maximum width of `13.75rem`.
- `.clipboard-board::before` / `::after` are bottom rivets. `.clipboard-clip::before` is clip hardware; preserve those pseudo-elements when extending the component.
- Shortcut anchors use a three-column internal grid: title, descriptor, `OPEN →`. Keep descriptors short enough for one line.
- The component uses `color-mix()`, gradients, and `aspect-ratio`; new pages that need older-browser support must provide fallbacks.
- Do not reuse `.hero-briefing` on another page without either supplying the same three-child layout or overriding its desktop grid.

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
- Every pack HTML page links `css/themes/facility.css` **directly**. Do not route the live theme through `css/style.css` or another `@import`.
- Keep the theme path relative. Root-absolute `/spt-pack/...` works in production but breaks the pack’s GitHub project Pages staging path.

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
