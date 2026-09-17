# Lifecycle and Races

Apply this guide to affected guards, defensive copies, cancellation, cleanup, or cross-boundary state, not an inventory of unrelated code.

For affected validators, copies, retries, rollbacks, or wrappers, name the failure prevented and lifetime covered. For affected flags, queues, callbacks, or controllers, name writers, readers, transitions, and cleanup. Adversarial tests can expose contract violations; passing tests alone does not prove lifecycle guarantees.

Consolidate only when ownership, transitions, and failure guarantees match. Atomic publication, rollback, callback isolation, terminal-state arbitration, worker ownership, and durable completion are distinct. If state is redundant, keep the copy the strictest consumer trusts.

`dispose`, abort, and stopped flags do not prove timers, listeners, streams, workers, promises, queued retries, or buffered writes have finished. Name what can still publish, persist, or call back after the terminal point. Cancellation is not quiescence.

Cut a branch only when its ordering guarantee survives elsewhere or has no consumer. Happy-path success does not prove canceled-before-start, mid-flight cancel, simultaneous endings, or repeated cleanup. Sleeps and stress runs cannot prove race freedom.
