# Agent knowledge (CampD-Website)

Modular context for Cursor agents. **Prefer adding files over editing existing ones.**

## Read order

1. [project.md](project.md) — stable facts (repo role, URLs, pipeline, paths)
2. [conventions.md](conventions.md) — git, accounts, editing rules
3. [design-chrome.md](design-chrome.md) — homepage vs SPT pack masthead, tokens, publish flow
4. [notes/](notes/) — chronological session/decision logs (newest filename last when sorted)
5. [handoffs/](handoffs/) — archive of briefings sent to other-repo agents (read if coordinating with CampD-SPT-Pack)

Skip re-reading old notes or handoffs if the task is narrow; read them when you need history or prior decisions.

## Add a note (do not rewrite baseline unless facts changed)

1. Create **one new file** in `agent/notes/`:
   - Name: `YYYY-MM-DD-short-topic.md` (ASCII, lowercase, hyphens)
   - Example: `2026-08-20-homepage-nav-tweak.md`
2. Use the template in [notes/README.md](notes/README.md).
3. Do **not** edit other agents’ note files.
4. Update [project.md](project.md) or [conventions.md](conventions.md) only when a **stable fact** changed (new URL, new workflow, path move). Put reasoning and narrative in your note instead.

## Related repos

| Repo | Agent docs |
|---|---|
| This site | `agent/` here |
| CampD-SPT-Pack | Pack repo root docs + [handoffs/](handoffs/) here for what we sent them; pack source, not `spt-pack/` here |

Local pack clone: `D:\My Documents\Projects\Games\Tarkov\CampD SPT Pack`
