# Pilot metrics

## Primary

- **Mergeable PRs in week 1:** at least 5.
- **Papercuts fixed in 30 nights:** at least 60.
- **Post-merge revert rate:** below 10%.

## Secondary

- **Median PR size:** below 100 changed lines.
- **Median time from reproduction to PR:** below 45 minutes.
- **Human review time per PR:** below 10 minutes.
- **Digest open rate:** above 80% among the pilot team.

## Guardrail metrics

- Zero changes outside the allowlist.
- Zero secrets in diffs or logs.
- Zero merges with red checks.
- Zero unreviewed database migrations.

## How the pilot is measured

Every run writes a JSON record with:

- candidate score
- source and evidence link
- files changed
- checks passed
- PR URL
- merge or revert outcome
- minutes of Devin compute used

The 30-day report aggregates these records and compares the result against the success criteria above.
