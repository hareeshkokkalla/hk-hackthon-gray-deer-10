---
name: Daily App Update
engine: copilot
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
tools:
  edit: {}
---

# Daily App Update

Update `index.html` with a dated daily update for this workflow run.

## Date and idempotency

1. Use the workflow run's UTC date, calculated at runtime with `date -u +%Y-%m-%d`.
2. Convert that date to the existing wording style, including the ordinal day and
   full month name, such as `1st of August`.
3. Inspect `index.html` before editing. If the UTC date or its matching date wording
   is already present, make no changes and finish successfully.
4. Do not duplicate an existing date, navigation control, or dialog.

## Required HTML changes

When the date is not already present, add one new item to the existing
`.daily-updates-list` navigation. Its button must:

- use the existing `daily-update-trigger` class;
- remain a `button` with `type="button"` and `aria-haspopup="dialog"`;
- use a unique date-based value in `aria-controls` matching the new dialog ID;
- include `data-dialog-trigger` so the existing script opens it; and
- display the date using the existing wording style, followed by the existing arrow.

Add a matching accessible `dialog` using the existing `.daily-update-dialog`
structure and styling. Follow the current ID conventions by using the date-based
slug for the dialog, question, and answer IDs. The dialog must:

- set `aria-labelledby` to its question heading ID;
- set `aria-describedby` to its answer paragraph ID;
- include the existing `daily-update-dialog-content`,
  `daily-update-dialog-header`, and `dialog-close` classes;
- show the same date in the header as the navigation item; and
- confirm that the daily update ran, using a concise question heading and answer.

Preserve the existing August 1 update and every other existing update. Keep the
existing inline dialog script unchanged. Do not modify `styles.css` or any file
other than `index.html`. Use the existing HTML entities, indentation, text style,
and accessibility attributes as a guide.
