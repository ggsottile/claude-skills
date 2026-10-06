# Writing the checklist into Coda / Superhuman Docs

Use the docs connector (tool names like `table_create`, `table_rows_manage`, `table_view_manage`, `content_read`). Load its `tool_guide` for the table and page topics first. Coda and Superhuman Docs use the same tools.

## Contents
- Steps
- Gotchas
- Optional: one checklist per brief

## Steps

1. **Resolve the page.** Decode the user's link with `url_convert` (scope `page`) to get the page URI. The text after `#` in a link is a block anchor, not a separate page.
2. **Read before writing.** `content_read` the page. Do not overwrite existing blocks. If a table is already there, ask whether to add below it or replace it.
3. **Create the table** with `table_create` on the page URI. Name it after the deliverable. Columns:
   - `Done`: `{"type": "check"}`
   - `Phase`: `{"type": "sl", "multiple": false, "selectOptions": [ ...phase names in workflow order ]}`
   - `Checklist item`: `{"type": "none"}`, width about 480
   - `Notes`: `{"type": "none"}`, width about 260. Plain text takes free notes and pasted links.

   Pass all rows in the same call (95 rows worked in one call). Each row is `["", "<Phase>", "<item>", ""]`. An empty string leaves Done unchecked and Notes empty. Later additions via `table_rows_manage` are limited to 100 rows per call.
4. **Views.** The table starts with one default view. Configure it, then add the other two:
   - Default view: rename to `Open items`, `sharedFilter` = `Not(Done)`.
   - Add `Completed items`, then configure `sharedFilter` = `Done`.
   - Add `All items`, then configure `groups.left` = `[Phase column id]` and `sorts` = Phase ascending. Grouping moves Phase into group headers and hides the column, which is fine. Sorting a select column should follow the option order, which is the workflow order. Check that in the UI.

   `table_view_manage` takes column ids, not names. Get them from the `table_create` result or `table_columns_read`.
5. **Verify.** `table_rows_read` should report the expected `totalRows`, with every Done false and Notes empty. Read the default view and confirm it shows all rows. Optionally tick one row, confirm it leaves `Open items` and appears in `Completed items`, then untick it.

## Gotchas

- **View names are unique across the whole doc.** Reusing "Open items" on a second table fails with "has already been used". Suffix with the checklist name, for example `Open items - Launch checklist`.
- A view added with `pageUri` (to embed the same table on another page) inherits the default view's filter. Set `sharedFilter` to `null` if you want it unfiltered.
- Bracket names in formulas resolve tables, views and controls only. Pages cannot be referenced by name.
- Only write to the page the user named. Do not create extra pages unless asked.

## Optional: one checklist per brief

Only set this up if the user asks for reusable copies. It is harder than it looks:

- Coda formulas cannot create a page, and `DuplicatePage` needs a page reference that cannot be typed into a formula. A button alone cannot spawn a sub-page.
- `content_duplicate` can be refused on docs where copying is not permitted ("User does not have permission to copy source document"). Rebuilding the page and table with `page_create` and `table_create` always works.
- The workable pattern in this workspace is a table with a button column that calls the **Doc Explorer** pack: `ModifyRows(thisRow, [Page id], [Doc Explorer]CreatePage([<account>], "<doc or page url>", [Brief name], ParentPageId: "<parent canvas id>"))`. A human has to install the pack in the doc and connect an account first. The API tools cannot resolve or test pack formulas, so write the formula text and ask the user to click-test it.
- The pack creates a blank page. The checklist table and views still have to be added to it, using the steps above.
- Keep the master table on its own sub-page and embed a view of it on the main page, so copies can start from a clean master.
