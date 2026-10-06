# Templates

Adapt to the repo. Replace `<…>` with real names; delete lines that don't apply.

## CLAUDE.md

```markdown
# <Repo name> — context layer

This repo is the context layer for <project>. Read `README.md` first: it says which file to
open for which job. Don't scan folders; the index is the map.

## Source of truth
- <topic>: `<file>` (supersedes anything else in the repo)
- <topic>: live in <Coda / n8n / tool>, not in this repo. `<file>` only describes it.

## Keep it current (every session)
At the end of any session that changed what's true, before the final reply:
1. **New file?** Add it to the README index: purpose + when to use it.
2. **Moved or renamed a file?** Update the README and grep for the old name; fix every hit.
3. **Found a fact that's wrong or stale?** Fix it at its source of truth. If you can't fix it
   now, add one line to README → "Known issues" with the date (DD.MM.YYYY).
4. **Learned something a future session needs** (an ID, a gotcha, a decision and its reason)?
   Put it in the file that owns that topic, not in a new notes file.
5. **Superseded a doc?** Mark it superseded in the index and point to the replacement. Don't
   delete it unless asked.
Keep edits small. Don't rewrite sections that are still right.

## Conventions
- Dates DD.MM.YYYY. <Other house rules: naming, folder for new prompts, etc.>
- Run /repo-cleanup when the index feels out of date.
```

## README skeleton

```markdown
# <Repo name>

<2–3 lines: what this repo is and who/what reads it.>

## Read this first
1. `<file>` — <why>
2. `<file>` — <why>

## Repo layout
<tree, one comment per folder>

## File index
| File | Type | Purpose | When to use |
|---|---|---|---|

## Known issues & cross-references
- <DD.MM.YYYY> <stale fact / conflict> → <what's true, where>

## Conventions & terminology
```
