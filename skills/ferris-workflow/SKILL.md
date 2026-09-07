---
name: ferris-workflow
description: Debug and verify behavior changes. Use when diagnosing failures, designing regression tests, proving deletions, or changing cancellation and shared state.
---

# Engineering Workflow

Check `git status` and leave unrelated work alone. A read-only request stays read-only. Commit, push, release, or repo-wide cleanup only when the user asked. Finish the requested outcome with verification proportional to the change; do not stop at a first draft.

| Task | Read |
|------|------|
| Failure, regression, crash, failing build/test, hang, or race | [references/debugging.md](./references/debugging.md) |
| Test design, doubles, or sensitivity | [references/tests.md](./references/tests.md) |
| Explicit cleanup or deletion audit | [references/cleanup.md](./references/cleanup.md) |
| Cancellation, resource cleanup, or cross-lifetime state | [references/lifecycle-and-races.md](./references/lifecycle-and-races.md) |

Before landing a diff, drop dead additions and debug debris in that diff. Broader cuts need the cleanup reference and an explicit scope.
