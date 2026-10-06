---
name: checklist-generator
description: Builds a short, evidence-based readiness checklist for a recurring deliverable (an ad, a release, a report, a delivery package) by mining the project's own history - Slack channels, email inboxes, Drive folders, spec docs, notes-to-self - for everything that was ever rejected, reworked, blocked or nearly missed, then writes the pruned checklist into a Coda / Superhuman Docs page. Use this whenever the user wants a pre-delivery or "before it goes live" checklist, a QA or definition-of-done list, wants to turn feedback history or past mistakes into a checklist, says things like "what do I need to check before X ships" or "we keep missing the same things", or asks to reconstruct what has to be verified for a deliverable - even if they never say "checklist" or name the sources.
---

# Checklist Generator

A checklist written from imagination is long, generic and ignored. A checklist written from project history is short, and every line exists because something went wrong once. This skill does two jobs, and both matter: research the history thoroughly, then cut the result hard. A list that is complete but padded fails as badly as a list that misses things, because people stop reading it.

## Workflow

### 1. Intake

Ask for what you can't already see in the conversation or attachments. Batch the questions in one go (use AskUserQuestion if available):

- **The deliverable**: what ships, to whom, how often (one-off or one per brief/release).
- **The project goal**: what "good" looks like for the client or end user.
- **The user's role**: which checks they personally do, and which they only have to chase. The checklist is for them, so items owned entirely by someone else are out unless the user must confirm them.
- **The finish line**: the moment the checklist protects (goes live, delivered, approved).
- **The Coda page link** where the final checklist goes. Required. Decode it and confirm you can read the page before doing anything else.
- **Spec or guideline documents** they already have (attach or link). Treat these as authoritative for hard rules.

### 2. Source access

The history lives in several places. Inventory them with the user, then prove access to each before reading anything:

| Source | Why it matters |
|---|---|
| Client-facing channels / shared inboxes | Shows what the client rejected or corrected |
| Internal channels | Shows what was nearly missed, and why |
| Notes-to-self / saved messages / a tag the user uses | Often the richest list of personal near-misses. Ask for the tag. |
| Drive / SharePoint folders, briefs, spec docs | Hard rules, past deliverable packages |
| Meeting notes, transcripts, task boards | Decisions and blockers that never reached chat |

Check your tool list (load deferred tools with ToolSearch) for Slack, Gmail/Outlook, Drive/SharePoint, Teams. Run one small test call per source. Then tell the user, in two lines, what works, what is missing, and what you need: channel names or IDs, folder links, a date window. If a source has no connector, ask for an export or a paste instead of skipping it silently. Confirm the scope (channels, folders, date range) before reading. Reading is read-only: never post, react or send anything in these sources.

### 3. Research

Go source by source and read whole threads, not snippets. The cause and the fix are usually in the replies. Log every issue that was raised as a blocker, rejection, rework, correction, delay or "please check" for this kind of deliverable. `references/research-playbook.md` has the search terms, the evidence-log format and a subagent brief for large sources. The short version:

- Log each issue in generalised form (what went wrong, what it cost, which phase should have caught it, how often, latest date, source link). Paraphrase. Never paste message text, private DMs or names of people who erred.
- Fan out with subagents when a source is large. Each returns log rows only, not transcripts.
- Recurrence and cost decide weight. Seen twice or costly: strong candidate. Seen once and cheap: weak.
- Stop at saturation: two more passes with different keywords and an older window add no new type of issue. Then say what you covered and what you could not reach.

Keep the evidence log in a working file. The checklist itself stays clean.

### 4. Synthesise and prune

Turn the log into candidate items, then prune. A first pass that still has 80+ items almost always has overlap. Apply every rule below. Full rules with before/after examples are in `references/pruning.md`.

**Keep an item only if all of these hold:**
- It has evidence in the history, or a spec or legal document requires it. "Good practice" with no evidence is cut.
- One person can tick it in a single sitting and point to proof. "Ensure quality" has no done-state. Cut it.
- It is a check on the deliverable or its inputs, not a process, habit or instruction about using the list.
- It belongs to the user's role, or the user has to confirm it.

**Merge, don't repeat:**
- Same check at several phases: keep it where catching it prevents the most rework. Add a second, final-verification copy only if the history shows it failing late.
- Inverted pairs ("only approved X appear" / "non-approved X do not appear") become one item.
- Conditional pairs ("if A is shown, do B" / "if A is not shown, omit B") become one item.
- A list split across rows (four deadlines, four rows) becomes one row.
- One-off incidents generalise to the recurring class ("player X left club Y" becomes "rosters are current for the season") or are dropped.

**Cut:**
- Continuous processes that never reach a finished state ("track all feedback").
- Meta-instructions ("record answers in the Notes column").
- Identifiers and links that belong in the page header, not the checklist.
- Unexplained acronyms. Spell them out in plain words or cut the item.

**Write each item** verb-first, one check, plain words, about 20 words or fewer, naming the specific thing. Order by workflow phase. Pick 6 to 10 phases from the deliverable's real lifecycle, in chronological order, ending with delivery. Do not reuse phase names from another project.

Before moving on, run the self-test on every item: if someone skipped it, would anything in the history have gone wrong again? If the honest answer is no, cut it.

### 5. Preview and confirm

Show the user, in chat: the phases, the numbered items per phase, and three counts (issues found in history, candidate items, final items). Add a compact cut log: each merged or dropped item with a one-line reason, so the user can veto a cut. Flag any item you are unsure about. One round of edits, then apply them. Nothing is written to Coda before this confirmation.

### 6. Write to Coda

Follow `references/coda-build.md`. In short: one table on the user's page with four columns (Done, Phase, Checklist item, Notes), every Done unchecked, every Notes cell empty, and three views: **Open items** (default, Done unchecked), **Completed items**, **All items** (grouped by Phase). Read the page first and do not overwrite what is already there. Afterwards, read back the row count and confirm the views behave.

### 7. Hand-off

Keep it to a few lines: the page link, the final item count against the issues found, one sentence on what was cut and why, any coverage gaps, and two offers: the evidence log as a file, and a per-brief copy setup if the deliverable recurs.

## What not to do

- Do not add requirements that have no evidence or spec behind them, however sensible they sound.
- Do not quote private messages or name individuals in the checklist or the cut log. Feedback addresses the action, not the person.
- Do not send messages to any channel or inbox you mined.
- Do not treat the first draft as done. The pruning pass is where most of the value comes from.
