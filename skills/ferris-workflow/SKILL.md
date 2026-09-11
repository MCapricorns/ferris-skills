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

## Debugging and regression checks

Capture the failing command, input, relevant error, and expected result. Find the smallest reliable repro; an obvious local defect needs no investigation tour. Trace to the first violated contract rather than hiding the symptom with a retry or timeout.

Check the symptom on unfixed code when feasible, without disturbing the user's work, and verify the fix with a regression check; reuse existing coverage when it catches the break. If the original trigger or environment is unavailable, state the evidence and verification gap. Proceed only when evidence supports the fix; do not guess or claim an unreproduced failure was reproduced.

Name the production break and exercise the smallest real boundary that owns it. Derive expectations independently of production helpers. Source-text and private-structure assertions are change detectors unless that representation is the contract; exact bytes or messages are valid when promised. A new or changed test must fail for the intended break, not setup.

Keep mocks at external or slow boundaries and model failures. For generated properties, include known examples or an independent oracle; matching encoder/decoder bugs survive a naive round trip. Control time, randomness, and resources; wait for an observable condition instead of sleeping a flake away.

## Cleanup and deletion proof

Remove dead additions and debug debris introduced by the current change. Use the deletion-proof guidance below for broader authorized cleanup or deletions. Cleanup may cut proven in-scope dead code without per-item approval; a review-only audit proposes cuts without making them.

- **Reachability:** classify candidate consumers as production, support-only, or unresolved. Check entrypoints, configuration, registration/reflection, codegen, string dispatch, external callers, and persisted keys where they apply. Tests and examples may document public contracts. Neither an empty search nor a green suite proves there are no consumers. Keep candidates with unresolved reachability and report the uncertainty; continue with other proven in-scope cuts.
- **Contract:** compare ownership, behavior, ordering, errors, and side effects, not textual similarity. Quiet history is not disuse. Name the behavior being surrendered and a check that would expose a mistaken cut.
- **Protected surfaces:** do not remove security controls, trust-boundary validation, accessibility, data-loss protection, durable compatibility, public APIs, or resource-quiescence cleanup without explicit approval covering that change. General cleanup authorization is not approval to weaken these guarantees. Generated/vendor files, fixtures, and migrations are not ordinary dead code.

Prefer deletion, then a canonical helper. Consolidate only matching contracts; keep feature logic in its owner. Do not move complexity behind another coordinator. Orchestration changes need understood independence, atomicity, ordering, and failure behavior.

Remove declarations, implementation, callers, config/exports/dependencies, dedicated tests, and affected docs together. Preserve coverage of surviving behavior and leave immutable history intact. Re-search removed names and run the checks that would catch a bad cut; repair or revert the change rather than weakening them. Persisted-data or shipped-artifact changes need a recovery path; a Git diff only reverses code.

## Lifecycle and races

Apply this section to affected guards, defensive copies, cancellation, cleanup, or cross-boundary state, not an inventory of unrelated code.

For affected validators, copies, retries, rollbacks, or wrappers, name the failure prevented and lifetime covered. For affected flags, queues, callbacks, or controllers, name writers, readers, transitions, and cleanup. Adversarial tests can expose contract violations; passing tests alone does not prove lifecycle guarantees.

Consolidate only when ownership, transitions, and failure guarantees match. Atomic publication, rollback, callback isolation, terminal-state arbitration, worker ownership, and durable completion are distinct. If state is redundant, keep the copy the strictest consumer trusts.

`dispose`, abort, and stopped flags do not prove timers, listeners, streams, workers, promises, queued retries, or buffered writes have finished. Name what can still publish, persist, or call back after the terminal point. Cancellation is not quiescence.

Cut a branch only when its ordering guarantee survives elsewhere or has no consumer. Happy-path success does not prove canceled-before-start, mid-flight cancel, simultaneous endings, or repeated cleanup. Sleeps and stress runs cannot prove race freedom.
