# Pack agent handoff — CSS @import load bug

- **Date:** 2026-08-15
- **Outcome:** handoff written; fix pending in CampD-SPT-Pack

## Summary

CampD sees pack pages sometimes stay on default browser styling (blue links, white background) until a normal refresh. Likely cause: `css/style.css` only `@import`s `themes/facility.css`. Fix is direct `<link>` to `facility.css` in pack HTML.

## Handoff file

Copy to pack project or pack agent chat: [PACK_AGENT_CSS_HANDOFF.md](../../PACK_AGENT_CSS_HANDOFF.md) at website repo root.

## Follow-ups

- [ ] Pack agent implements fix, push, Sync SPT Pack on website.
