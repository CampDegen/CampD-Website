# SPT two-repo decision and agent handoff

- **Date:** 2026-08-15
- **Agent context:** CampD-Website agent (cloud VM, then local on CampD machine)
- **Outcome:** done

## Summary

CampD briefly planned to merge CampD-SPT-Pack into this repo and delete the pack repo. That was a misunderstanding. The correct design is **two repositories**: pack repo is source; this repo mirrors public files into `spt-pack/` via GitHub Action. Agent-only markdown (`SPT_MERGE_KNOWLEDGE.md`, `SPT_AGENT_HANDOFF.md`) lived here temporarily, then was removed from this repo after the handoff was copied to the pack project.

## Decisions

- **Keep two repos.** Do not merge pack into website. Do not delete CampD-SPT-Pack.
- **Keep** `.github/workflows/sync-spt-pack.yml` on this repo.
- **Forge updater stays** on CampD-SPT-Pack (`scripts/update-forge-status.mjs`, pack workflow).
- **Handoff delivered** to `D:\My Documents\Projects\Games\Tarkov\CampD SPT Pack\SPT_AGENT_HANDOFF.md` (pack agent should align pack README/knowledge there; not this repo).
- **Website docs for humans:** `README.md` describes Pages + sync pipeline.
- **Website docs for agents:** `agent/` folder (this modular system). Removed root SPT_*.md files — history lives in this note.

## Follow-ups

- [ ] Pack repo agent: rewrite pack `SPT_MERGE_KNOWLEDGE.md` and README merge paragraph to match two-repo model (if not done yet).
