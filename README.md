# Nightshift

**An always-on Devin Bot that clears the backlog nobody prioritizes.**

> The bottleneck isn't coding. It's remembering.

Nightshift is a pilot spec for the Poke × Cognition Devin Bots challenge. It is designed to run every night on a real repository, ship small fixes while the team sleeps, and report back before standup.

## The problem

Every team has a list of small, real problems that never make it into a sprint:

- a flaky test that everyone reruns
- an error affecting 15 users
- a docs page with a broken code sample
- a `TODO` from eight months ago
- a papercut bug that is too small to prioritize

They compound quietly. Nobody owns them because everyone assumes someone else will.

## What Nightshift does

Every night at 02:00:

1. **Collect** open signals from Sentry, failed CI runs, GitHub issues, Linear tickets labeled `papercut`, and stale docs.
2. **Score** each candidate: `affected_users × frequency / effort`.
3. **Reproduce** the top candidate in a cloud browser or test harness.
4. **Fix** it with the smallest safe diff, adding a regression test first.
5. **Open a PR** with evidence, risk notes, and a rollback plan.
6. **Merge** only when all required checks pass and every changed file is on the allowlist.
7. **Report** at 07:00 with a Slack digest, PR links, and a one-click undo.

## Why this needs a Devin Bot

A human-triggered coding agent still depends on a human to notice, prioritize, and follow up. Nightshift removes that dependency. It is always on, has its own cloud computer, and uses the same tools a person would: Sentry, GitHub, Linear, and Slack.

The value is not a smarter model. The value is coverage.

## Guardrails

Nightshift is default-deny.

- Maximum 3 PRs per night.
- Only touches allowlisted paths (`src/`, `app/`, `packages/`, `tests/`, `docs/`).
- Never touches auth, billing, payments, infra, migrations, secrets, or CI workflows.
- No dependency upgrades in v1.
- No database writes.
- Every fix ships with a regression test.
- Merges only if lint, typecheck, and tests pass.
- Auto-reverts if post-merge checks fail.
- Daily budget cap and a kill switch (`NIGHTSHIFT_PAUSED=1`).
- If uncertain, comment and stop. Do not guess.

The full rules live in [`nightshift.config.yml`](./nightshift.config.yml).

## Pilot plan: 30 nights

| Phase | Scope | Success |
|---|---|---|
| Week 1 | Public repo, 7 nightly runs | 5 mergeable PRs |
| Week 2 | Private repo, 10 runs | 10 mergeable PRs, median PR < 100 lines |
| Weeks 3–4 | 13 runs | 60 papercuts fixed, revert rate < 10% |

Every digest is published. Every PR is auditable.

## Credit math

`$200 ≈ 30 nightly runs`

- ~60 papercuts fixed
- ~30 engineer-hours saved
- ~$2,400 of engineer time at $80/hour
- ~12× return on the credit grant

The backlog compounds, so the ROI compounds with it.

## What is in this repo

- [`nightshift.config.yml`](./nightshift.config.yml) — budget, allowlist, denylist, checks, and escalation rules
- [`prompts/nightshift.md`](./prompts/nightshift.md) — the Devin Bot operating prompt
- [`templates/digest.md`](./templates/digest.md) — the 07:00 Slack digest
- [`templates/pr.md`](./templates/pr.md) — the PR body template
- [`docs/metrics.md`](./docs/metrics.md) — how the pilot is measured

## Commitment

If Nightshift does not produce 5 mergeable PRs in the first week, I will:

1. return the unused credits,
2. publish a public postmortem, and
3. explain exactly which assumption failed.

## Status

`v0.1` — pilot spec. Ready to connect to a repository.