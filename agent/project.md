# Project baseline

Stable facts. Change only when the repo or pipeline actually changes. Put story and reasoning in `notes/`.

## Role

**CampDegen/CampD-Website** — GitHub Pages host for [campdegen.com](https://campdegen.com/). Static site: no build step, no `dist/`. `main` is what Pages serves.

## Live URLs

| URL | Source |
|---|---|
| `/` | `index.html`, `css/styles.css`, `assets/` |
| `/spt-pack/` | `spt-pack/` — **mirror**, not edited here |

Custom domain: `CNAME` → `campdegen.com`. Only this repo may use that domain.

## Local paths (CampD machine)

| | Path |
|---|---|
| Website clone | `D:\My Documents\Projects\CampD\Websites\Current\CampD-Website` |
| Pack clone (source) | `D:\My Documents\Projects\Games\Tarkov\CampD SPT Pack` |

## SPT pack pipeline (two repos — intentional)

Pack **source**: [CampDegen/CampD-SPT-Pack](https://github.com/CampDegen/CampD-SPT-Pack).

```
CampD-SPT-Pack  06:00 UTC  Forge Action → data/forge-status.json
CampD-Website   06:30 UTC  Sync SPT Pack → replaces spt-pack/, commits
Pages                       campdegen.com/spt-pack/
```

Workflow: `.github/workflows/sync-spt-pack.yml`

**Copied into `spt-pack/`:** `index.html`, `settings.html`, `looking.html`, `css/`, `js/`, `data/`, `assets/`

**Not copied (pack repo only):** `.github/`, `scripts/`, `reference_data/`, pack README

Sync **deletes and recreates** `spt-pack/` each run. Never hand-edit `spt-pack/` in this repo.

Manual sync: Actions → **Sync SPT Pack** → Run workflow.

Pack staging Pages: `https://campdegen.github.io/CampD-SPT-Pack/` (optional mirror). Production: campdegen.com.

## Identity / design

- Colors: `colors.md` (semantic token names); live aged hex in `css/styles.css`
- Homepage typography: Bebas Neue, Rajdhani, Share Tech Mono
- Brand assets: `NOTICE` — not MIT-licensed
- Chrome rules (homepage vs `/spt-pack/`): [design-chrome.md](design-chrome.md)

**Header behavior:** homepage `.site-header` is sticky. Homepage header tabs: Overview, Communications. SPT Pack is on the hero clipboard index. Pack pages use the same masthead styling but `position: relative` so the bar scrolls away. Pack has no site nav tabs in the masthead; Mods / Pack Settings / Looking to add use `.pack-nav` below the header.

## Human docs

Site operator README: [../README.md](../README.md)
