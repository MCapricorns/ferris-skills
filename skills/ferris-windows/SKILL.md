---
name: ferris-windows
description: Windows contracts. Use when tasks hinge on paths, encoding, DLL loading, elevation, Win32/COM/PInvoke, or PowerShell 7 argument handling.
---

# Windows Engineering

Default to Windows and PowerShell 7 (`pwsh`) for house development and command examples. Use another host, Windows PowerShell 5.1, or cmd/batch only when the task or repository requires it.

Read the relevant sections of [references/rules.md](./references/rules.md). Runtime behavior wins over house defaults; do not apply every Windows rule to a shell-only task.

## Shell execution

- Chain success-dependent native commands with `&&`. Use explicit status handling only for special exit-code contracts or recovery. Cmdlet error handling is separate.
- Use argument arrays and literal paths. PowerShell is not a POSIX shell.
