# Cleanup and Deletion Proof

Remove dead additions and debug debris introduced by the current change. Use the deletion-proof guidance below for broader authorized cleanup or deletions. Cleanup may cut proven in-scope dead code without per-item approval; a review-only audit proposes cuts without making them.

- **Reachability:** classify candidate consumers as production, support-only, or unresolved. Check entrypoints, configuration, registration/reflection, codegen, string dispatch, external callers, and persisted keys where they apply. Tests and examples may document public contracts. Neither an empty search nor a green suite proves there are no consumers. Keep candidates with unresolved reachability and report the uncertainty; continue with other proven in-scope cuts.
- **Contract:** compare ownership, behavior, ordering, errors, and side effects, not textual similarity. Quiet history is not disuse. Name the behavior being surrendered and a check that would expose a mistaken cut.
- **Protected surfaces:** do not remove security controls, trust-boundary validation, accessibility, data-loss protection, durable compatibility, public APIs, or resource-quiescence cleanup without explicit approval covering that change. General cleanup authorization is not approval to weaken these guarantees. Generated/vendor files, fixtures, and migrations are not ordinary dead code.

Prefer deletion, then a canonical helper. Consolidate only matching contracts; keep feature logic in its owner. Do not move complexity behind another coordinator. Orchestration changes need understood independence, atomicity, ordering, and failure behavior.

Remove declarations, implementation, callers, config/exports/dependencies, dedicated tests, and affected docs together. Preserve coverage of surviving behavior and leave immutable history intact. Re-search removed names and run the checks that would catch a bad cut; repair or revert the change rather than weakening them. Persisted-data or shipped-artifact changes need a recovery path; a Git diff only reverses code.
