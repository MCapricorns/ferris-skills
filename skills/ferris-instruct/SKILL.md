---
name: ferris-instruct
description: Authors or reviews SKILL.md, AGENTS.md, CLAUDE.md, and other standing agent instructions. Use when changing those files or diagnosing how they change agent behavior. Not for ordinary code edits.
---

# Agent Instruction Authoring

## Ownership

- One rule, one owner. The always-on file (AGENTS.md, CLAUDE.md) owns authority, approvals, communication, secrets, and habits for every task. A skill owns task-specific depth and restates a general rule only where its own advice could erode it.
- When two files say the same thing, delete the non-owner's copy; when they disagree, fix the conflict instead of adding a tie-breaker. Check what actually loads (symlinks, per-host copies) before deleting.
- Repository packaging rules and validation commands go in repository docs, not a portable skill.

## Writing for current models

Current models follow instructions closely and generalize from intent, so extra emphasis backfires:

- Write the delta over model knowledge: house preferences, consequential traps, and ordering that matters. Cut tutorials, generic caution, and restated defaults.
- State a rule once, plainly, with its reason when non-obvious. Capitals, repeated NEVER/MUST, and stacked caveats cause over-application and needless refusals.
- Do not turn one past failure into a universal gate, and delete workarounds for models no longer in use. Keep committed instructions model-neutral.
- Give exact commands only when variation is a defect; otherwise state the outcome and the constraint. Use a script for deterministic work instead of pasting it into the prompt.

## Skills

- The description may be shortened in a large catalog. Lead with the action and the situation in the user's words, in third person or imperative. Add an exclusion only when a neighboring skill would claim the request. No keyword lists, and no trigger that fires on every edit or commit.
- A new skill needs a distinct, recurring trigger. Omit optional frontmatter unless every consumer parses it the same way.
- Keep guidance in SKILL.md; move detail to a one-level-deep reference only when it is substantial and unused on most activations.

## What a standing file should settle

Precedence (user over file over skills, within host permissions); read-only versus implementation scope; when to ask versus decide; which actions need approval and that approval is reused; finishing through the authorized endpoint; and naming the rule behind any pause. Each in a line, once.

## Verifying changes

Try matching requests, near misses, and requests that belong to a neighboring skill; check completion and authorization behavior, not just selection. Packaging checks prove loading, not effectiveness. When auditing, cite the wording and its concrete consequence, and keep deletion proof, security boundaries, and meaningful checks when shortening.
