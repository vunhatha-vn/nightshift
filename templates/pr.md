## What changed

{{one_sentence_summary}}

## Evidence

- Source: {{source}}
- Link: {{source_link}}
- Affected users: {{affected_users}}
- Observed frequency: {{frequency}}

## Root cause

{{root_cause}}

## Fix

{{fix_summary}}

## Regression test

{{test_name}} — fails on `main`, passes on this branch.

## Risk and blast radius

{{risk_summary}}

## Rollback

Revert this PR with `git revert {{commit_sha}}`. No data migration is involved.

## Checklist

- [ ] Change is limited to allowlisted paths
- [ ] Regression test added
- [ ] Lint, typecheck, and tests pass
- [ ] No secrets or customer data in the diff
- [ ] Rollback is a single revert
