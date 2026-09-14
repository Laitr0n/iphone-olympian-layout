# Unjiggle Workflow

Use this reference only for device inspection, layout rewrites, backup, or restore work.

## Read and Classify

- Use the Python environment where `unjiggle` is installed; install it only if necessary and permitted.
- Start with a read-only scan of the current layout.
- Treat web clips as classifiable items, not disposable extras.
- Treat widgets as top-level widgets; do not place widget bundle identifiers inside folders.
- Build a deterministic layout plan that assigns every non-Dock app or web clip exactly once.

## Write Safely

- Exclude Dock bundle IDs from every folder so Dock order is preserved.
- Preserve first-page widgets by copying raw widget items into the target page.
- For iOS 26 folder raw objects, use `{"displayName": name, "iconLists": pages, "listType": "folder"}`. The `listType: "folder"` field is required.
- Use 9 icons per internal folder page unless there is a clear reason to do otherwise.
- Before writing, run a static coverage check: no duplicates, no missing visible non-Dock apps, no extra nonexistent bundle IDs.
- Call Unjiggle's verified backup before `write_layout`.

## Verify

After writing, read the layout again and verify:

- page count is still 1 when that was requested,
- total app count matches the pre-write layout,
- Dock bundle-id sequence equals the backup's Dock bundle-id sequence,
- folder names match the planned Olympian list.

Report what changed, the final page/app count, Dock verification, and the backup path.
