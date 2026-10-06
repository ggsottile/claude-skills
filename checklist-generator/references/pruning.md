# Pruning rules

The first draft of a checklist built from project history is always too long. In the run that inspired this skill, the first draft had 95 items and was later cut by hand, mainly for duplicates and items nobody could act on. The patterns below are the ones to catch automatically. The examples come from that first draft and show the pattern. They are illustrations, not a record of what was actually removed.

## Contents
- Overlap across phases
- Inverted pairs
- Conditional pairs
- Split lists
- Not checkable
- Meta-instructions
- Generic hygiene with no evidence
- Vague scope
- One-off incidents
- Acronyms
- Wording

## Overlap across phases

The same check appears at planning, at the work itself and at final QA.

Before (three rows):
- Confirm every featured player belongs to the correct current-season club roster.
- Confirm every visible opponent player belongs to the correct current-season club roster.
- Re-check every visible player and background player against current rosters before sending the draft.

After (one row, placed before the work starts, where a miss costs a recapture):
- Every visible player, featured, opponent or background, is on their club's current-season roster.

Keep a second copy at final QA only if the history shows the error slipping through late.

## Inverted pairs

- Confirm only approved ambassadors appear in EA kits.
- Confirm non-ambassadors do not appear in EA kits.

After: Only approved ambassadors wear EA kits.

## Conditional pairs

- If gameplay is shown, confirm the disclaimer is used as required.
- If gameplay is not shown, confirm the disclaimer is omitted.

After: The in-game disclaimer appears only when gameplay is shown.

## Split lists

Four rows for capture deadline, first-draft deadline, final-delivery deadline and go-live date become: Confirm go-live, capture, first-draft and final-delivery dates.

## Not checkable

Items with no finished state. "Track every feedback item to completion and record the resolving version" never ticks. Either cut it or turn it into a state someone can verify: "No open feedback items at final approval."

## Meta-instructions

"Record the client's answers in the Notes column" is advice on using the list, not a check on the deliverable. Cut.

## Generic hygiene with no evidence

"Confirm priority against every other open brief" and "Reserve a buffer slot" sound sensible, but if nothing in the history shows them going wrong they are padding. Cut unless the log has a matching issue.

## Vague scope

"List every ambiguity, contradiction and requirement in the brief" is an open-ended task, not a check. Replace it with something concrete ("Open questions on the brief are sent to the client before production starts") or cut it.

## One-off incidents

A single incident (one named player left one named club) generalises to the class it belongs to (rosters current for the season), or it is dropped. The checklist should prevent the next incident of the same kind, not repeat the last one.

## Acronyms

If the team needs a glossary to read the item, the item is not ready. Spell the acronym out in plain words, or cut the item if it is not something the user owns.

## Wording

- Verb-first, one check per item, about 20 words or fewer.
- Name the specific thing ("end-slate call to action"), not the category ("branding").
- Plain words. No filler lead-ins such as "ensure that" or "make sure to".
- Order by phase, earliest first.

## Self-test, every item

Would skipping this item let something in the history happen again? Could one person tick it in one sitting and show proof? Does it fall in the user's role? Three yeses keep it. Anything else is cut or merged.
