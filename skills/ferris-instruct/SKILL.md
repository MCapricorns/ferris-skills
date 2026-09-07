---
name: ferris-instruct
description: Author and audit agent instructions. Use when changing SKILL.md, AGENTS.md, or standing prompts, or reviewing their behavior.
---

# Agent Instruction Authoring

## Scope and loading

Keep durable project constraints in AGENTS.md and task-specific workflows in skills. Keep repository-specific packaging rules and validation commands in repository instructions, not a portable skill. Check actual loading before removing duplicate safety or approval rules; a distributed skill cannot assume the user's global instructions.

A skill description says what it does, then **when** for the concrete action, not the surrounding domain. Prefer `Use when adding or changing a migration, or reviewing its rollout` to `Use when working with databases`. Avoid keyword stuffing, overlapping triggers, and loading a portable skill before every edit or commit. A new skill needs a distinct, recurring trigger.

Keep compact guidance in SKILL.md. Split substantial, independently useful detail into references only when on-demand reading saves context; do not force a router or a separate file for a paragraph. Link references directly from the entry point.

Do not prescribe an itinerary for routine work. Keep house preferences, consequential traps, and steps whose ordering matters. Point at project docs only when the task needs them; a typo does not require an architecture tour.

## Authorization and clarification

- Requests for review or analysis alone are read-only; an explicit request to review and fix authorizes in-scope edits. Implementation requests authorize necessary in-scope code, tests, docs, configuration, and non-destructive validation.
- Make routine, reversible choices from available evidence. Ask when missing information materially changes the outcome, requirements conflict, or an explicit approval boundary applies. Explain the concrete decision and recommendation; group blocking questions and continue independent authorized work.
- Preserve authorization requirements for commits, pushes, releases, deployments, destructive actions, and unrelated changes. A requested action includes routine in-scope prerequisites, not broader or destructive actions. Reuse approval already given rather than demanding the same approval at each step.
- Do not turn ordinary design trade-offs or a user's explicit scope change into a mandatory confirmation gate. Do not silently substitute a materially different outcome.

## Completion and verification

Finish the requested outcome rather than stopping after a first draft. If the request includes running, inspecting, committing, or pushing the change, carry out the authorized steps. A blocked step does not end safe independent work; report the blocker and remaining work without claiming full completion. Persistence does not authorize scope expansion.

Preserve required repository checks and meaningful assertions. Scale other verification to the change; repeat or broaden only for new changes, failures, or unresolved concerns. Disposable local tests without production access can run, be repaired for change-caused failures, and rerun without repeated approval.

Small behavioral changes still need checks sensitive to the break. Do not require tests that merely mirror implementation details or documentation wording unless that representation is itself the contract. Packaging checks establish loading and link validity, not instruction effectiveness.

When auditing, cite the file and original wording, explain a concrete consequence, and distinguish necessary safety/approval requirements from accidental friction. Shorter text must preserve regression sensitivity, deletion proof, security/compatibility boundaries, and meaningful checks. If a rule blocks completion, distinguish an explicit requirement from the agent's interpretation.

Sources: [OpenAI model guidance](https://developers.openai.com/api/docs/guides/latest-model?model=gpt-6-astra) and [Eric Provencher](https://x.com/pvncher/status/2095991462416490862).
