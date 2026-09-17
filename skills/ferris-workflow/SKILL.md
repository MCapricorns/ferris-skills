---
name: ferris-workflow
description: Debug and verify behavior changes. Use when diagnosing failures, designing regression tests, proving deletions, or changing cancellation and shared state.
---

# Engineering Workflow

Plain wording, formatting, and Git-message edits do not need this skill; do not make it a prerequisite for every edit or commit.

## Execution boundaries

Reviews and analysis alone are read-only; a request to implement or review and fix authorizes necessary in-scope changes and non-destructive validation. Check `git status` in a worktree and preserve unrelated work. Do not commit, push, release, deploy, or perform destructive or unrelated actions without user authorization; reuse authorization already given.

Never read credential stores, expose or commit secrets, or dump the environment; inspect only task-relevant non-secret settings. Do not weaken existing security, approval, data-loss, or compatibility guarantees without explicit approval.

## Verification scope

Preserve required repository checks and meaningful assertions. Scale other verification to the change and reuse existing checks that cover the affected behavior. Add or change tests when needed to cover that behavior; avoid tests that merely mirror the implementation. Repeat or broaden checks only for new changes, failures, or unresolved concerns. Report checks actually run, distinguish unrelated failures from change-caused failures, and identify verification gaps.

Add or change CI only for an explicit request or a concrete project verification need; use existing project tooling where suitable. A Git repository alone does not justify adding GitHub Actions. Preserve required checks when changing automation.

## Task guides

| Task | Read |
|------|------|
| Diagnosing a failure or writing a regression check | [references/debugging.md](./references/debugging.md) |
| Authorized cleanup or deletion | [references/deletion.md](./references/deletion.md) |
| Cancellation, cleanup ordering, or shared state | [references/lifecycle.md](./references/lifecycle.md) |
