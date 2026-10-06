# Research playbook

## Contents
- Signal words
- Evidence log format
- Subagent brief for large sources
- Saturation check
- Coverage report

## Signal words

Search each source with several of these. Different people phrase the same problem differently, so run a wide set and read the surrounding thread every time.

- Rejection and correction: rejected, not approved, wrong, incorrect, outdated, old, no longer, doesn't match, should be, must be, needs to be, please change, fix, revert
- Rework: redo, re-do, recapture, reshoot, re-export, re-render, resend, again, second time, v2, new version, replace
- Blockers and delays: blocked, waiting on, pending, stuck, can't, unable, missing, not available, delayed, late, deadline, slipped
- Checks and reminders: please check, double check, make sure, don't forget, reminder, before we, always, never, rule, guideline, requirement
- Approvals: approved, sign-off, legal, licensing, partner, brand, feedback, comments
- Also the user's own tag in notes-to-self, if they have one.

Adapt the list to the project's domain. Add the terms the people in this project actually use (product names, asset types, tool names).

## Evidence log format

Keep it as a markdown table in a working file, one row per distinct issue.

| # | Issue (generalised, one line) | Type | Phase it should have been caught | Times seen | Cost | Latest date | Source ref |
|---|---|---|---|---|---|---|---|

- Type: rejection, rework, blocker, near-miss, spec rule.
- Cost: delay, recapture/rework, client rejection, none observed.
- Source ref: a permalink or file name. No quoted text.

Merge rows that describe the same issue and add to "Times seen". This table feeds the pruning pass, so keep it honest about how often each issue recurred.

## Subagent brief for large sources

When a channel, mailbox or folder is big, hand it to a subagent:

> Read [source] between [dates]. Find every message or document where something for [deliverable type] was rejected, corrected, reworked, blocked or flagged as "needs checking". Read full threads. Return only evidence-log rows in this format: [table header]. Generalise each issue, paraphrase, no quoted text, no names of people who made the mistake. Include a permalink for each row. Finish with one line listing what you could not access.

Run one subagent per source so they work in parallel, then merge the rows yourself.

## Saturation check

After the first full pass, run two more: one with different keywords, one over an older date window or a different source. If neither adds a new type of issue, the research is saturated. If they do, repeat.

## Coverage report

Finish research with three lines for the user: sources read (with date ranges), sources not reachable, and whether saturation was reached. The user needs this to judge what the checklist might still miss.
