---
name: ferris-workflow
description: Debugs and verifies behavior changes. Use when diagnosing a failure, designing a regression test, proving a deletion, or changing cancellation and shared state. Not for wording, formatting, or commit-message edits.
---

# Engineering Workflow

## Debugging

- Capture the failing command, input, error, and expected result, then find the smallest reliable repro. An obvious local defect needs no investigation tour.
- Fix the first violated contract, not the symptom; a retry or longer timeout is not a fix.
- Confirm the symptom on unfixed code when feasible without disturbing the user's work. If the trigger is unavailable, say what evidence supports the fix and what stays unverified.
- When reading configuration, read only task-relevant, non-secret settings.

## Regression tests

- Exercise the smallest real boundary that owns the break, and derive expected values independently of production helpers.
- A new test must fail for the intended break, not for setup. Assertions on source text or private structure are change detectors unless that representation is the contract.
- Mock only external or slow boundaries. Round-trip tests need known vectors or an independent oracle; matching encoder and decoder bugs cancel out.
- Control time and randomness; wait on an observable condition, never a sleep.
- Keep required repository checks; distinguish change-caused failures from pre-existing ones.

## Deletion proof

Remove debris the current change introduced without ceremony. For broader authorized cleanup, cut proven dead code without per-item approval; a review-only audit proposes cuts instead.

- **Reachability:** check entrypoints, config, registration and reflection, codegen, string dispatch, external callers, and persisted keys. An empty search or a green suite does not prove absence. Keep and report candidates with unresolved reachability.
- **Contract:** compare behavior, ordering, errors, and side effects, not textual similarity. Name the behavior being surrendered and the check that would catch a wrong cut.
- **Protected surfaces:** security controls, trust-boundary validation, accessibility, data-loss protection, durable compatibility, public APIs, and resource cleanup need approval for that specific change. Generated or vendored files, fixtures, and migrations are not ordinary dead code.

Remove declarations, callers, config, exports, dependencies, dedicated tests, and docs together; re-search removed names. Prefer deletion over a new abstraction, and consolidate only identical contracts. Persisted-data or shipped-artifact changes need a recovery path; a Git revert only restores code.

## Lifecycle and races

Scope this to the guards, copies, cancellation, cleanup, or shared state the change touches.

- For each affected flag, queue, callback, or controller, name its writers, readers, transitions, and cleanup. For each validator, copy, retry, or rollback, name the failure it prevents.
- Cancellation is not quiescence: after `dispose`, abort, or a stopped flag, timers, listeners, workers, promises, queued retries, and buffered writes may still publish or call back. Name what can.
- Consolidate state only when ownership and failure guarantees match; if redundant, keep the copy the strictest consumer trusts.
- Test canceled-before-start, mid-flight cancel, simultaneous completion, and repeated cleanup. Passing tests, sleeps, and stress runs do not prove race freedom.
