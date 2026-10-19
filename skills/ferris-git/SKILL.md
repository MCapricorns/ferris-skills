---
name: ferris-git
description: Resolves Git merge and rebase conflicts, recovers lost work, performs requested history rewrites, and fixes line-ending, attribute, and submodule problems. Use when Git state is tangled or a history operation is requested. Not for routine commits.
---

# Git Repair and History

## Before touching history

- Note the tip SHA of each branch you will move. The reflog recovers commits, not working-tree edits: after `reset --hard`, `restore`, `clean`, or `stash drop`, only previously staged content survives, as dangling blobs (`git fsck --lost-found`). Commit or stash the user's work first.
- There is no interactive editor. Use `--no-edit`, `commit --fixup` with `rebase --autosquash`, and `rebase --onto`; otherwise set `GIT_SEQUENCE_EDITOR`/`GIT_EDITOR` to a non-interactive command. Stage partial hunks with `git apply --cached`, not `add -p`.

## Conflicts

- Read both sides' intent first: `git log --merge -p -- <path>`, and `git checkout --conflict=zdiff3 -- <path>` to show the base. Wholesale `--ours`/`--theirs` is right only when one side is intentionally dropped.
- Lockfiles and generated files: take one side, then regenerate with the owning tool from the merged inputs, without a blanket update.
- A clean textual merge can still be a semantic conflict; build and run checks covering both sides.

## Requested rewrites

- Keep authorship and commit boundaries unless asked otherwise. `--update-refs` keeps stacked branches attached.
- Push with `--force-with-lease --force-if-includes`, never bare `--force`.
- In `git bisect run`, exit 125 means skip; make setup failures exit 125 so they are not marked bad.

## Repository state traps

- `.gitattributes` `text`/`eol` rules override `core.autocrlf`. After changing them, renormalize (`git add --renormalize .`) in its own commit.
- With `core.fileMode=false` (Windows default), set executable bits with `git add --chmod=+x`.
- With `core.symlinks=false`, a symlink checks out as a text file holding its target; do not commit it as content.
- For `dubious ownership`, add the specific path to `safe.directory`, never `*`; it is a global config change.
- Submodule pointer moves are real changes; do not commit accidental ones.
- A file starting with `version https://git-lfs` is an unfetched LFS pointer; never commit it over real content.
