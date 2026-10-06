---
name: repo-cleanup
description: Audits and tidies a repo that serves as the context layer for AI sessions (a knowledge base, "brain" repo, docs-and-prompts repo), so later sessions find things from the README in one hop and spend fewer tokens. Sends a mini-audit with a proposed fix for every problem, applies only what the user approves, sets up CLAUDE.md upkeep rules so future sessions keep the context layer current, then commits and asks before pushing. Use when the user types /repo-cleanup, or asks to tidy, audit, clean up or reorganise a context/knowledge repo, fix its README index, or make it cheaper for Claude to navigate.
---

# Repo Cleanup — context-layer audit

The goal is a repo where a fresh session reads `CLAUDE.md` (auto-loaded), then `README.md`, and
knows exactly which one file to open next. Every wasted file read, wrong path and duplicate doc
costs tokens on every future session.

Work in four phases. **Never change a file before Phase 3 approval.**

## Phase 1 — Scan (read-only)

Collect facts cheaply. Prefer one shell pass over many tool calls.

1. `git status --short`, `git log --oneline -5`, `git fetch` then `git log --oneline HEAD..@{u}`
   (remote commits not yet local).
2. Full file list excluding `.git` and anything gitignored, with sizes.
3. Read `README.md`, `CLAUDE.md`, `AGENTS.md`, `.gitignore`, `.gitattributes` and any nested READMEs in full.
4. For every other file, read only the first ~15 lines (title + purpose). Read in full only when
   checking a suspected duplicate.
5. Extract every path the README (and CLAUDE.md) mentions; check each exists.
6. Grep the repo for cross-references to file names, so you know what breaks if something moves.

## Phase 2 — Audit (send to user, then stop)

Check every item in the checklist below. Output the audit **in chat** in this shape, then wait:

```
## Repo audit — <repo name>
<one line: overall state + count of issues by severity>

| # | Sev | Problem | Proposed fix | Risk |
|---|-----|---------|--------------|------|
| 1 | High | README indexes `X-3.md`; real file is `X.md` | Fix the path in the index | None |
| 2 | Med  | ... | ... | Breaks 2 refs in prompts/ — updated in the same change |

**Not touching:** <things that look odd but are fine, and why>
**Needs your call:** <decisions only the user can make, e.g. delete vs archive>

Reply "all", a list of numbers, or "none".
```

Severity: **High** = sends a future session to the wrong or missing file, or loses work
(broken index paths, untracked files, stale facts presented as current). **Med** = wastes
tokens or causes confusion (duplicates, strays, unindexed files, no CLAUDE.md). **Low** = naming
and cosmetic issues.

Every problem gets a concrete fix. If the fix is risky (deletes, moves with inbound
references), say so in Risk and offer the safe alternative (archive/move instead of delete).

### Checklist

**Entry points**
- `CLAUDE.md` exists at the root, is short (under ~60 lines), and contains the upkeep rules
  (template in `references/templates.md`). It points to README rather than repeating it.
- `README.md` opens with 2–3 lines on what the repo is, then a "read this first" order, then
  a layout tree, then a file index.
- One README per folder at most; nested READMEs only where the folder has its own conventions.
  A stray `README-1.md` / `README (2).md` is a misplaced file — move it or merge it.

**Index accuracy**
- Every file the README mentions exists at exactly that path.
- Every non-trivial file is indexed, with **purpose** and **when to use it**. A session must be
  able to pick the right file from the index alone, without opening candidates.
- Superseded docs are marked as superseded in the index, with a pointer to what replaced them.
- Known-stale facts (a doc that disagrees with production, an old figure) are flagged in one
  "Known issues / cross-references" section, not scattered.

**Duplicates & strays**
- Near-duplicate names (`file (1).txt`, `file-3.md`, `final_v2`) — diff them; keep one.
- Upload/export suffixes in names that no longer mean anything.
- Files sitting in the wrong folder (a sprint prompt in root while `prompts/` exists).
- Generated output committed that should be gitignored (build output, chunks, `out-*`).
- Empty files and folders; OS junk (`.DS_Store`, `Thumbs.db`, `desktop.ini`).

**Structure**
- Folders group by job (reference / scopes / prompts / outputs / tools), not by date.
- Numbered sequences (prompts, steps) have titles that match their file numbers.
- **Do not move files that other docs reference by name** unless you update every reference
  in the same change. When references are many, keep the layout and document why in README.
- Prefer flat over deep: a session should reach any file within two hops of the README.

**Token cost**
- Huge files (>~50 KB of text) that sessions would read whole: suggest splitting, or adding a
  short summary/ToC at the top so a session can stop early.
- Raw dumps (exports, transcripts, CSVs) sit in a clearly named data folder and are indexed as
  "open only when you need the raw numbers".
- The same fact maintained in several files: name one source of truth, link to it from the others.

**Git hygiene**
- Untracked or uncommitted work (flag as High: one bad session can lose it).
- Local branch behind its remote.
- Line-ending config present on Windows repos (`.gitattributes`).

## Phase 3 — Apply (only what was approved)

1. Apply approved fixes in this order: moves/renames → reference updates → content fixes →
   README → CLAUDE.md. Use `git mv` for tracked files so history follows.
2. After moves, re-grep for the old names; zero hits allowed outside the git log.
3. Re-run Phase 1 step 5: every README/CLAUDE.md path must resolve.
4. Create or update `CLAUDE.md` from `references/templates.md`, adapted to this repo
   (real folder names, real source-of-truth files). Keep anything the user had already written.
5. Write README changes in the repo's existing voice. Don't rewrite sections that were fine.

## Phase 4 — Commit, then ask before pushing

1. `git add -A` and one commit: `Tidy context layer: <short list of changes>`.
2. Report what changed in a few bullets and what was deliberately left alone.
3. Ask before pushing. On push rejection: fetch, show the user the incoming commits, then
   `git pull --rebase` (never force-push). Check that the remote's edits survived, then push.

## Principles

- Audit first, change second. No silent fixes.
- Archive or move rather than delete. Delete only on an explicit yes for that file.
- Never touch secrets, `.env` files, or credentials. If one is committed, report it as High
  and recommend rotating it; don't try to rewrite history.
- Reports to the user stay short and plain. The table is the audit; skip preamble.
