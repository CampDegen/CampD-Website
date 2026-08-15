# Handoff for the CampD-SPT-Pack agent — two-repo model

Supersedes merge-and-delete in `SPT_MERGE_KNOWLEDGE.md`.

**Delivered** 2026-08-15. Authoritative copy for the pack agent: `SPT_AGENT_HANDOFF.md` in CampD-SPT-Pack. This file is the website-repo archive.

## What CampD thought

That the pack had to live as real source files inside CampD-Website, that the copy-sync was a temporary bridge, and that CampD-SPT-Pack should be deleted after a merge.

## What is actually true (authoritative)

Two GitHub repos, on purpose, going forward.

| Repo | Job | Do not |
|---|---|---|
| **CampDegen/CampD-SPT-Pack** | Source of the pack. Edit catalog JSON, themes, scripts, Forge Action here. | Do not delete this repo. Do not move Forge/scripts onto the website. |
| **CampDegen/CampD-Website** | Public site (`campdegen.com`). Homepage is native. `spt-pack/` is a **mirror** filled by GitHub Action. | Do not treat host `spt-pack/` as the place to edit the pack. Sync will wipe hand-edits. |

GitHub Pages allows **one CNAME** (`campdegen.com`) on **one** repo (CampD-Website). The website Action clones this pack repo and copies public files into `spt-pack/`. That pipeline is correct, not a leftover.

## Pipeline (keep this)

```
CampD-SPT-Pack  06:00 UTC  Forge Action  →  commit data/forge-status.json
CampD-Website   06:30 UTC  Sync Action   →  rm -rf spt-pack, clone this repo,
                                            copy public files, commit if changed
GitHub Pages                              →  https://campdegen.com/spt-pack/
```

Copied: `index.html`, `settings.html`, `looking.html`, `css/`, `js/`, `data/`, `assets/`.

Not copied: `.github/`, `scripts/`, `reference_data/`, README, knowledge files.

Manual sync: CampD-Website → Actions → **Sync SPT Pack** → Run workflow.

## Pack agent follow-ups (at time of handoff)

1. Rewrite `SPT_MERGE_KNOWLEDGE.md` and README merge paragraph for two repos.
2. Keep Forge updater in pack repo.
3. Chrome work in pack repo; sync publishes to campdegen.com.

## Accounts / git

- CampDegen = GitHub **User**. Loneranger419 is collaborator.
- Do not `git config`. Commit with `git -c user.name=Loneranger419 -c user.email=113032413+Loneranger419@users.noreply.github.com`.
