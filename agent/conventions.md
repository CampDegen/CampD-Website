# Conventions

## Git / GitHub

- GitHub user **CampDegen** (User account, not org). Collaborator: **Loneranger419**.
- Do not run `git config` (global or local).
- Commit as Loneranger419 when human-owned work:
  ```
  git -c user.name=Loneranger419 -c user.email=113032413+Loneranger419@users.noreply.github.com ...
  ```
- Do not force-push `main`.

## Where to edit

| Change | Edit here | Not here |
|---|---|---|
| Homepage, site chrome | `index.html`, `css/styles.css` | — |
| SPT catalog, pack UI, mod JSON | CampD-SPT-Pack repo | `spt-pack/` (sync overwrites) |
| Forge version data | CampD-SPT-Pack (script + Action) | — |
| Agent context / history | `agent/notes/` (new file) | Avoid rewriting old notes |

## Do not

- Merge CampD-SPT-Pack into this repo (decision: keep two repos + sync).
- Add a second Pages custom domain for campdegen.com.
- Hand-edit `spt-pack/` while sync workflow exists.
- Copy Forge listing text into mod descriptions (pack repo rule).

## Agent docs maintenance

- New session or decision → new file under `agent/notes/`.
- Update `agent/project.md` only for factual drift (paths, URLs, workflow names).
- Root `KNOWLEDGE.md` stays a pointer; do not bloat it.
