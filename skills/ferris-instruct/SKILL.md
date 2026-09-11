---
name: ferris-instruct
description: Author or audit SKILL.md, AGENTS.md, and standing prompts when changing their instructions or diagnosing how they affect agent behavior.
---

# Agent Instruction Authoring

## Scope and loading

Keep durable project constraints in AGENTS.md and task-specific workflows in skills. Keep repository-specific packaging rules and validation commands in repository instructions, not a portable skill. Check actual loading before removing duplicate safety or approval rules; a distributed skill cannot assume the user's global instructions.

A skill description leads with the concrete action and when it applies, so it still routes correctly if shortened. Prefer `Use when adding or changing a migration, or reviewing its rollout` to `Use when working with databases`. Avoid keyword stuffing, overlapping triggers, and loading a portable skill before every edit or commit. A new skill needs a distinct, recurring trigger.

Keep compact guidance in SKILL.md. Split substantial, independently useful detail into references only when on-demand reading saves context; do not force a router or a separate file for a paragraph. Link references directly from the entry point.

Keep house preferences, consequential traps, and steps whose ordering matters. Leave routine implementation choices open. Do not turn one past failure into a universal gate or add tools, scripts, or references without a concrete need.

## Authorization and clarification

- State that user instructions take precedence over skill guidelines, within higher-priority instructions and host permissions. A skill must not silently expand scope, replace the requested outcome, or imply permission for external actions.
- Requests for review or analysis alone are read-only; an explicit request to review and fix authorizes in-scope edits. Implementation requests authorize necessary in-scope code, tests, docs, configuration, and non-destructive validation.
- Make routine, reversible choices from available evidence. Ask when missing information materially changes the outcome, requirements conflict, or an explicit approval boundary applies. Explain the concrete decision and recommendation; group blocking questions and continue independent authorized work.
- Preserve authorization requirements for commits, pushes, releases, deployments, destructive actions, and unrelated changes. A requested action includes routine in-scope prerequisites. Reuse existing authorization; when approval is still needed, finish authorized preparation first so the user can review the concrete result.
- If an instruction causes a pause, confirmation request, incomplete work, or a change from the user's intent, name and link to the exact file, quote the relevant instruction, and explain its effect. Distinguish explicit requirements from interpretation; ordinary trade-offs and user-authorized scope changes are not new approval gates.

## Completion and verification

Treat action-implying requests as work to complete. Carry out requested running, inspecting, committing, or pushing through the authorized endpoint. Keep the original objective when incorporating follow-up corrections or answering side questions, unless the user cancels or replaces it. A blocked step does not end independent authorized work; report the blocker and remaining work without claiming completion or expanding scope.

Describe when available subagents improve independent work, with bounded ownership and an integration check; do not make delegation a prerequisite for routine tasks. Specify concise, outcome-first communication and enough evidence to explain material limitations.

Preserve required repository checks and meaningful assertions. Scale other verification to the change; repeat or broaden only for new changes, failures, or unresolved concerns. Disposable local tests without production access can run, be repaired for change-caused failures, and rerun without repeated approval.

Small behavioral changes still need checks sensitive to the break. Avoid tests that merely mirror implementation details or documentation wording unless that representation is itself the contract. For changed instructions, try realistic matching and nearby non-matching requests, checking task completion and authorization as well as selection. Use an independent behavioral pass when complexity warrants it. Packaging checks establish loading and link validity, not instruction effectiveness.

When auditing, cite original wording and a concrete consequence. Preserve regression sensitivity, deletion proof, security/compatibility boundaries, and meaningful checks when simplifying instructions.

Sources: [OpenAI Astra guidance](https://developers.openai.com/api/docs/guides/latest-model?model=gpt-6-astra) and [OpenAI skill authoring](https://learn.chatgpt.com/docs/build-skills).
