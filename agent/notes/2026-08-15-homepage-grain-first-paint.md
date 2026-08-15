# Homepage aging overlay skipped first paint

- **Date:** 2026-08-15
- **Agent context:** local, CampD-Website
- **Outcome:** done on homepage; pack still uses SVG noise (handoff)

## Summary

CampD’s “blue until refresh” is on **campdegen.com/**, not a missing stylesheet. Both screenshots show full layout/fonts. The cooler (blue-gray) visit is first paint without the film-grain + vignette layers; a normal refresh composites them and the page looks warm/aged.

Cause: grain was `body::before` with an SVG `feTurbulence` **data-URI** background. Chromium often does not paint that filter until a later pass. The `@import` pack-theme fix does not address this.

## Changes (this repo)

- Real overlay nodes in `index.html`: `.film-grain`, `.vignette`.
- Grain tile: `assets/grain.png` (no SVG filter).
- `html { color-scheme: dark; }` to stop a bluish UA canvas.
- Do not restore `feTurbulence` data-URIs for overlays.

## Follow-ups

- [ ] Pack `css/themes/facility.css` still uses the same SVG data-URI. See [handoff](../handoffs/2026-08-15-pack-grain-png.md).
