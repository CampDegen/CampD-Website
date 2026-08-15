# SPT pack theme linked directly

- **Date:** 2026-08-15
- **Agent context:** local (pack source + website documentation)
- **Outcome:** done — pack `ca99cd3`, website sync `fb9d873`

## Summary

Pack pages sometimes persisted with browser-default styling. Their only stylesheet was a tiny `css/style.css` wrapper that introduced a second request for the real facility theme through `@import`. The exact intermittent failure was not captured, but direct linking removes that likely failure point.

## Changes

- Pack `index.html`, `settings.html`, and `looking.html` now link `css/themes/facility.css` directly.
- The URL stays relative so both `campdegen.com/spt-pack/` and `campdegen.github.io/CampD-SPT-Pack/` work.
- Pack `css/style.css` is retained only as a compatibility shim for cached old HTML; current pages do not reference it.
- Pack README and agent knowledge describe the new theme-switch process.

## Do not

- Do not change the pack theme URL to root-absolute `/spt-pack/...`; that breaks GitHub project Pages staging.
- Do not reintroduce a `style.css` → `@import` chain on live pack pages.
- Do not hand-edit this repo’s `spt-pack/` mirror. Publish by pushing the pack and running **Sync SPT Pack**.
