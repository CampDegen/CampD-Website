# Homepage clipboard shortcut index

- **Date:** 2026-08-15
- **Outcome:** done

## Summary

SPT Pack moved out of the sticky header and onto a physical-looking shortcut index in the homepage hero. The component uses a dark, oil-worn WWII-style wood/hardboard back, metal clip, ruled Letter paper, and boxed links. “SPT Pack — Mod catalog” is one clickable row with an `OPEN →` cue.

During iteration, bottom-aligning the three-column grid moved the logo down. Stretching a narrow clipboard also overrode its declared ratio and rendered it around 1:2. The final layout explicitly top-aligns the emblem and lets clipboard width determine an exact US Letter ratio.

## Decisions

- Header contains Overview + Communications only.
- Desktop clipboard column: `19rem` to `20.75rem`.
- Clipboard ratio: exact `8.5 / 11`; do not force `height: 100%`.
- Hero emblem stays `align-self: start`.
- Desktop `.clipboard` override must follow its base rule in CSS.
- Shortcut entries use title + short descriptor + `OPEN →` on one line.
- Add later shortcuts as new list items; do not add more system links to the header.

## Reconstruction

Stable markup, selectors, breakpoints, and cross-page CSS caveats are documented in [`../design-chrome.md`](../design-chrome.md#homepage-clipboard-index).
