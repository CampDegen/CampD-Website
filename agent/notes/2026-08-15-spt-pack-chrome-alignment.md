# SPT pack chrome aligned with homepage

- **Date:** 2026-08-15
- **Agent context:** CampD-SPT-Pack agent (local)
- **Outcome:** done (pack repo); website mirror pending sync

## Summary

Pack pages were restyled to match campdegen.com aged background and masthead. Homepage keeps sticky header + site nav tabs; pack subpages use the same masthead chrome without those tabs, scroll with the page, and put Mods / Pack Settings in `.pack-nav` under the header.

## Decisions

- **Background:** Pack `facility.css` uses the same aged `:root` hex and body gradient/grain/vignette as website `css/styles.css`, not the digital-native values from `colors.md` alone.
- **Masthead:** Logo + `CampD` + `header-meta` doc strip (CD-SPT-PACK / page label / SPT version). No Overview, SPT Pack, or Communications in pack header.
- **Sticky:** Homepage `.site-header` remains sticky. Pack `.site-header` is `position: relative` so it scrolls off on subpages.
- **Scale fix:** Moved `font-size: 1.125rem` from `html` to `body` on pack pages so rem-based header matches homepage size.
- **All pack HTML/CSS changes** live in CampD-SPT-Pack; this repo receives them only via **Sync SPT Pack**.

## Pack commits (reference)

- `82ef691` — match background + masthead; pack-local nav
- `b0c1a53` — non-sticky header + rem scale fix

## Follow-ups

- [ ] Run **Sync SPT Pack** on CampD-Website after pack pushes so `spt-pack/` mirror matches.
- [ ] Pack repo: OG/Twitter tags, footer parity with `.site-footer` (optional).
