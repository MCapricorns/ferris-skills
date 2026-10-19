# ferris-skills

Five engineering skills plus one instruction-authoring skill, focused on house choices and easily missed contracts, not language tutorials or generic coding advice. Compatible with the [Agent Skills format](https://agentskills.io/specification), including Pi and Claude Code.

Primary development environment: **Windows with PowerShell 7 (`pwsh`)**. Command examples use PowerShell; other hosts and legacy shells are compatibility targets, not defaults.

## Skills

| Skill | Use for |
|-------|---------|
| [ferris-workflow](skills/ferris-workflow/SKILL.md) | Diagnosing a failure, writing a sensitive test, proving a deletion, or changing cancellation and shared state |
| [ferris-native](skills/ferris-native/SKILL.md) | C++/Rust ownership, unsafe/FFI, async cancellation, or compiler/linker and Cargo/MSBuild failures; separate C++ and Rust references |
| [ferris-windows](skills/ferris-windows/SKILL.md) | Windows paths, encoding, DLL loading, elevation, Win32/COM/PInvoke, or PowerShell 7 commands |
| [ferris-git](skills/ferris-git/SKILL.md) | Conflicts, lost-work recovery, requested history rewrites, and line-ending, attribute, or submodule problems |
| [ferris-perf](skills/ferris-perf/SKILL.md) | Profiling, benchmarking, and backing a speedup or memory claim with numbers |
| [ferris-instruct](skills/ferris-instruct/SKILL.md) | Adding, editing, or reviewing SKILL.md, AGENTS.md, or other always-on agent instructions |

Load by task, not by chain: a Python regression needs workflow, not native; Linux Rust needs no Windows rules; a routine commit loads no skill.

## Design rules

- **Delta over model knowledge.** Keep house preferences and consequential traps; cut tutorials, generic caution, and restated defaults. Say each rule once, plainly; stacked MUST/NEVER wording makes current models over-apply it.
- **One rule, one owner.** The user's always-on AGENTS.md/CLAUDE.md owns authority, approvals, communication, secrets, and commit format. Skills own task depth: workflow owns diagnosis, tests, and cleanup; native owns language contracts; Windows owns platform behavior; git owns repair and history; perf owns measurement; instruct owns standing instructions. A new skill needs a distinct, recurring trigger.
- **Precise triggers, compact bodies.** Descriptions lead with the action and situation in third person or imperative and add an exclusion only against a neighboring skill. Split into a reference only for substantial detail unused on most activations.
- **Preserve guarantees.** Shorter text keeps regression sensitivity, deletion proof, security/compatibility boundaries, and meaningful checks.

Frontmatter uses only `name` and `description`, both single-line plain scalars without `: ` or ` #`; names match their directories. After changing skills, README listings, or the validator, run `python scripts/validate_skills.py`; CI runs the same packaging checks, which do not measure model effectiveness.

## Install and update

Interactive installation selects skills, agents, and scope:

```powershell
npx skills add github:MCapricorns/ferris-skills
```

List, install all globally, or update global installations:

```powershell
npx skills add github:MCapricorns/ferris-skills -l
npx skills add github:MCapricorns/ferris-skills -s '*' -g
npx skills update -g -y
```

Use `-s <name>` (for example `-s ferris-git`) to select one skill. Add `--copy` if symlinks are unsuitable. Manual installation: copy desired `skills/<name>/` directories into `~/.agents/skills/` or the agent's own skill directory. Reload skills or restart the agent after updating.

### Migrating from six skills

`ferris-audit`, `ferris-debug`, and `ferris-tests` become `ferris-workflow`; `ferris-cpp` and `ferris-rust` become `ferris-native`; `ferris-windows` keeps its name. Updating existing names may not install replacements or remove retired names. Install replacements for the same agents/scope before removing old names:

```powershell
npx skills add github:MCapricorns/ferris-skills -s ferris-workflow ferris-native ferris-windows -g
npx skills remove ferris-audit ferris-debug ferris-tests ferris-cpp ferris-rust -g
```

Update explicit references in agent/project instructions and reload. No compatibility stubs keep retired triggers active.
