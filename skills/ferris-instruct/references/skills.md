# Skill Files

A skill is a workflow the model needs only for some tasks, or instructions for a plugin. Name and description load with every other skill, every session.

## Description

One clause of what it does, then **when** for the concrete action. Not the surrounding domain.

- Bad: `Create and validate Postgres schema migrations. Use when working with databases, queries, models, or persistence.`
- Good: `Create and validate Postgres schema migrations. Use when adding or changing a migration, or reviewing its rollout.`

No keyword stuffing, no "before every commit," no grab for a neighbor skill's work. Too many skills, or long overlapping descriptions, get truncated and start contradicting each other.

## Shape

The root file is a router. Give enough to pick a reference or script; do not load every workflow on every hit. House rules that apply to every use of the skill may stay in the root; everything else is on-demand.

Do not write an itinerary for work the model can already do. Guidance that helped a weaker model can overconstrain a stronger one. Prefer house preferences and consequential traps.

## Local contracts

Keep repository-specific packaging rules and validation commands in repository instructions, not a portable skill.

Shorter text must keep regression sensitivity, deletion proof, security/compatibility boundaries, and meaningful checks. A new skill needs a distinct, recurring trigger.
