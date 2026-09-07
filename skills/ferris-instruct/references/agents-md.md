# AGENTS.md

Keep durable project constraints here and task-specific workflows in skills. Check actual loading before removing duplicate safety or approval rules; a distributed skill cannot assume the user's global instructions.

## Read what the task needs

- Bad: `Before every edit, read architecture.md, database.md, and deployment.md.`
- Good: `Use architecture.md for service boundaries, database.md for schema changes, and deployment.md when preparing a deployment.`

Do not require a repo map or a doc stack for a typo. Point at a doc only when that change needs it, and keep the doc current.

## Checks

Preserve required repository checks and meaningful assertions. Scale other verification to the change; once checks pass, repeat or broaden only for new changes, failures, or unresolved concerns. Do not require tests that merely mirror reversible, low-impact edits.

For a local suite that uses disposable fixtures and has no production access, it is enough to say: run it, fix failures caused by the requested change, and rerun the affected tests without asking at each step.
