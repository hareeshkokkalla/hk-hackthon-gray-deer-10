---
name: Weekly Report Status
engine: copilot
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly repository activity report

Create a concise activity report for this repository covering the previous seven
calendar days relative to the workflow run. Use the GitHub context and available
GitHub tools to review:

- commits pushed to the repository;
- issues opened, closed, or otherwise materially updated; and
- pull requests opened, closed, merged, or otherwise materially updated.

Summarize the results in a new issue using clear headings and short bullet lists.
Include the reporting period at the top of the issue and link to relevant commits,
issues, and pull requests when available. State clearly that no activity occurred
in any category with no matching events. If there was no activity at all, say so
clearly in the report rather than omitting the issue.

Publish the report using the configured `safe-outputs.create-issue` output. Do not
make any other repository changes or write to existing issues.
