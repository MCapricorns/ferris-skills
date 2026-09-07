# ferris-skills

Three engineering skills plus one instruction-authoring skill, focused on house choices and easily missed contracts, not language tutorials or generic coding advice. Compatible with the [Agent Skills format](https://agentskills.io/specification), including Pi and Claude Code.

Primary development environment: **Windows with PowerShell 7 (`pwsh`)**. Command examples use PowerShell; other hosts and legacy shells are compatibility targets, not defaults.

## Skills

| Skill | Use for | Guidance |
|-------|---------|----------|
| [ferris-workflow](skills/ferris-workflow/SKILL.md) | Diagnosing a failure, writing a sensitive test, proving a deletion, or simplifying lifecycle/races | Execution boundaries, debugging/tests, deletion proof, and lifecycle/races in SKILL.md |
| [ferris-native](skills/ferris-native/SKILL.md) | C++/Rust ownership, unsafe/FFI, async cancellation, or compiler/linker and Cargo/MSBuild failures | Separate C++ and Rust references; read both for mixed-language boundaries |
| [ferris-windows](skills/ferris-windows/SKILL.md) | Windows paths, encoding, DLL loading, elevation, or Win32/COM/PInvoke | Shell, paths, DLL search, encoding, privilege, and GUI sections in SKILL.md |
| [ferris-instruct](skills/ferris-instruct/SKILL.md) | Adding, editing, or reviewing SKILL.md, AGENTS.md, or other always-on agent instructions | Authoring, authorization, clarification, and completion in SKILL.md |

Load by task, not by chain: a Python regression needs workflow, not native; Linux Rust needs no Windows rules; a compiler fix does not load instruct. References link directly from their entry point.

## Design rules

- **Keep the delta over model knowledge.** House preferences and consequential traps stay; syntax tutorials, investigation itineraries, and generic caution do not.
- **Precise triggers, compact bodies.** Descriptions say what the skill does and when to use it, not the whole domain or "before every commit." Keep concise guidance in SKILL.md; split only substantial, independent detail that benefits from on-demand reading.
- **One concern, one owner.** Workflow owns diagnosis/tests/cleanup, native owns language contracts, Windows owns platform behavior, instruct owns standing agent instructions. Do not add a fifth skill for a one-off.
- **Finish authorized work.** Make routine reversible choices, reuse existing approvals, and do not stop after a first draft. Ask for consequential missing decisions or explicit approval boundaries; a blocked step does not end safe independent work. Repository conventions win over house defaults; check current vendor docs when adopting a feature.
- **Preserve guarantees.** Shorter text must keep regression sensitivity, deletion proof, security/compatibility boundaries, and meaningful checks.

See the official [skill-authoring guidance](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) for concision and progressive disclosure.

In this repository, frontmatter uses only `name` and `description`, both single-line plain scalars. Avoid `: ` and ` #` in their values; names match their directories.

After changes to skills, README skill listings, or the validator, run `python scripts/validate_skills.py`. CI uses the same validator for frontmatter/YAML safety, naming/description limits, local references, orphan references, and README coverage. It checks packaging, not model effectiveness.

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

Use `-s ferris-workflow` or `-s ferris-instruct` to select one skill. Add `--copy` if symlinks are unsuitable. Manual installation: copy desired `skills/<name>/` directories into `~/.agents/skills/` or the agent's own skill directory. Reload skills or restart the agent after updating.

### Migrating from six skills

`ferris-audit`, `ferris-debug`, and `ferris-tests` become `ferris-workflow`; `ferris-cpp` and `ferris-rust` become `ferris-native`; `ferris-windows` keeps its name. Updating existing names may not install replacements or remove retired names. Install replacements for the same agents/scope before removing old names:

```powershell
npx skills add github:MCapricorns/ferris-skills -s ferris-workflow ferris-native ferris-windows -g
npx skills remove ferris-audit ferris-debug ferris-tests ferris-cpp ferris-rust -g
```

Update explicit references in agent/project instructions and reload. No compatibility stubs keep retired triggers active.
