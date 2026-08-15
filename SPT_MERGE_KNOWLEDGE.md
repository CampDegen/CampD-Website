# SPT_MERGE_KNOWLEDGE

Agent-only. **Supersedes merge-and-delete.** CampD walked that back: two repos are the intended design.

Handoff for the pack-repo agent: [SPT_AGENT_HANDOFF.md](SPT_AGENT_HANDOFF.md). Human pipeline notes: [README.md](README.md).

## End state (authoritative)

Keep **CampDegen/CampD-SPT-Pack** and **CampDegen/CampD-Website**. Do not merge the pack into the website. Do not delete the pack repo. Do not remove `.github/workflows/sync-spt-pack.yml`.

| Piece | Where it lives |
|---|---|
| Live pack URL | `https://campdegen.com/spt-pack/` (Pages on this repo, folder `spt-pack/`) |
| Pack source | CampD-SPT-Pack (edit there) |
| Forge updater | CampD-SPT-Pack `.github/workflows/update-forge.yml` + `scripts/update-forge-status.mjs` |
| Website mirror | this repo `spt-pack/` filled by Sync SPT Pack |
| Homepage | this repo `index.html` / `css/styles.css` |

## Why two repos + a copy

GitHub Pages: one CNAME (`campdegen.com`) → one repo (CampD-Website). A second Pages custom domain for this hostname is not allowed. Path `/spt-pack/` is a folder on the website. The pack stays its own repo so catalog/Forge work is not mixed into homepage commits. Website Action clones the pack and copies public files. That is publish, not a temporary bridge.

## Pipeline (do not replace)

```
CampD-SPT-Pack 06:00 Forge Action → commit forge-status.json
CampD-Website  06:30 Sync Action  → rm -rf spt-pack, clone pack repo, copy public files, commit
Pages                             → campdegen.com/spt-pack/
```

Public copy set: `index.html`, `settings.html`, `css/`, `js/`, `data/`, `assets/`.

Not copied: pack `.github/`, `scripts/`, `reference_data/`, pack README, pack knowledge files.

`GITHUB_TOKEN` cannot write the other repo. No PAT. Sync is destructive on host `spt-pack/` — never hand-edit that folder here.

## Repos / paths / accounts

| Role | Repo | Local |
|---|---|---|
| Site host | CampDegen/CampD-Website | `D:\My Documents\Projects\CampD\Websites\Current\CampD-Website` |
| Pack source | CampDegen/CampD-SPT-Pack | `D:\My Documents\Projects\Games\Tarkov\CampD SPT Pack` |
| Pack staging Pages | github.io/CampD-SPT-Pack | optional mirror; live is campdegen.com |

- CampDegen = GitHub **User** (not org).
- Commit/push as **Loneranger419**. Do not `git config`. Use `git -c user.name=Loneranger419 -c user.email=113032413+Loneranger419@users.noreply.github.com`.
- Identity: host `colors.md` / pack `reference_data/colors.md`. Token **names** matter. Type: Bebas Neue, Rajdhani, Share Tech Mono.

## Chrome / pack UI

Do pack chrome work **in CampD-SPT-Pack**, then let sync publish. Do not restyle host `spt-pack/` in this repo while sync exists.

Relative URLs inside the pack (`css/style.css`). Host-wide: `/`, `/spt-pack/`, `/#about`, `/#connect`.

## Do not

- Delete CampD-SPT-Pack or move Forge onto this repo.
- Hand-edit host `spt-pack/` (sync wipes it).
- Second Pages custom domain for campdegen.com.
- Forge listing text in descriptions.
- `git config` changes, force-push `main`.
