# SPT pack Looking to add page

- **Date:** 2026-08-15
- **Agent context:** local (pack + website)
- **Outcome:** done in pack + website workflow docs; live after pack push and Sync SPT Pack

## Summary

Added `/spt-pack/looking.html` for old-server mods that are not on the current 4.1.2 pack. Host sync must copy `looking.html` as well as `index.html` and `settings.html`. Data lives in pack `data/looking-to-add.json` (Forge ids after name matching; `id` null if unverified).

## Decisions

- Source edits stay in CampD-SPT-Pack. Website only mirrors.
- Sync workflow copies `looking.html` into `spt-pack/` on each run.
- Forge updater on the pack repo also fetches looking-to-add ids.

## Follow-ups

- [ ] Push pack + website workflow, then run **Sync SPT Pack**.
