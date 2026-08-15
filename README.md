# CampD Website

Public site for [campdegen.com](https://campdegen.com/). This is a **static** GitHub Pages project. There is no npm/webpack compile, no generated `dist/`. What is in this repo on `main` is what Pages serves.

## What goes live

GitHub Pages is enabled on **CampDegen/CampD-Website**. Custom domain is [`CNAME`](CNAME) → `campdegen.com`. Only this repo may use that domain.

| URL | Source in this repo |
|---|---|
| `https://campdegen.com/` | [`index.html`](index.html), [`css/styles.css`](css/styles.css), [`assets/`](assets/) |
| `https://campdegen.com/spt-pack/` | [`spt-pack/`](spt-pack/) — **not edited here** (see below) |

Colors and type: [`colors.md`](colors.md). Branding in [`NOTICE`](NOTICE) is not covered by the MIT [`LICENSE`](LICENSE).

Local preview (needed so `/spt-pack/` JSON `fetch` works):

```bash
python -m http.server 8080
```

Then open `http://localhost:8080/` and `http://localhost:8080/spt-pack/`.

## How the SPT pack gets onto this site

The pack is a **separate repository**: [CampDegen/CampD-SPT-Pack](https://github.com/CampDegen/CampD-SPT-Pack). Local clone: `D:\My Documents\Projects\Games\Tarkov\CampD SPT Pack`. That repo is the source (mod list, settings, Forge version check, pack CSS/JS). This website clone: `D:\My Documents\Projects\CampD\Websites\Current\CampD-Website`.

This website does not build the pack. A GitHub Action **copies** the pack’s public files into `spt-pack/` and commits if they changed.

```
CampD-SPT-Pack   06:00 UTC   Forge Action updates data/forge-status.json
CampD-Website    06:30 UTC   Sync SPT Pack clones the pack repo, replaces spt-pack/, commits
GitHub Pages                 serves https://campdegen.com/spt-pack/
```

Workflow: [`.github/workflows/sync-spt-pack.yml`](.github/workflows/sync-spt-pack.yml)

Copied from the pack repo: `index.html`, `settings.html`, `looking.html`, `css/`, `js/`, `data/`, `assets/`.

Not copied (stay only in the pack repo): Forge script, pack GitHub Actions, `reference_data/`.

Pack pages link `css/themes/facility.css` directly with a relative URL. Do not reintroduce the former `css/style.css` → `@import` chain in the pack source or hand-edit the mirrored HTML here.

The sync **deletes and recreates** `spt-pack/` every run. Do not hand-edit files under `spt-pack/` on this repo; the next sync will overwrite them. Edit the pack repo instead, then wait for the daily sync or run it manually:

GitHub → this repo → **Actions** → **Sync SPT Pack** → **Run workflow**.

The pack repo also has a staging Pages site at `https://campdegen.github.io/CampD-SPT-Pack/`. Live production is always campdegen.com.

## Editing the homepage

Change [`index.html`](index.html) and [`css/styles.css`](css/styles.css) in this repo and push `main`. Pages updates from that. SPT Pack is linked from the hero clipboard index (`/spt-pack/`, trailing slash), not the header. To add another shortcut, add a matching list item to `.clipboard-list`; reconstruction and responsive CSS constraints are in [`agent/design-chrome.md`](agent/design-chrome.md#homepage-clipboard-index).

## Agent documentation

Cursor agents: read [`KNOWLEDGE.md`](KNOWLEDGE.md) first, then [`agent/`](agent/). Stable facts: `agent/project.md`, `agent/conventions.md`, `agent/design-chrome.md`. Session history: `agent/notes/`. Outbound briefings to other repos: `agent/handoffs/`.
