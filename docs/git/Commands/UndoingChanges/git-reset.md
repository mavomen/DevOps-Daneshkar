---
id: git-reset
aliases: []
tags: []
---

# git reset

Move a branch/ref (and optionally update index/working directory) to undo commits or unstage changes.

## Syntax

```bash
git reset [<mode>] <commit>
git reset [<mode>] <commit> -- <pathspec>...
```

Common modes:

- `--soft`
- `--mixed` (default)
- `--hard`

## Description

`git reset` changes where the current branch (and `HEAD`) points.

Depending on mode, it can also update:

- the staging area (index)
- the working directory

This makes it powerful and potentially destructive.

If you need a safe undo on shared history, consider [[git-revert]].

## Basic Usage

### Reset last commit but keep changes staged

```bash
git reset --soft HEAD~1
```

### Reset last commit and unstage changes (keep working changes)

```bash
git reset HEAD~1
# same as:
git reset --mixed HEAD~1
```

### Reset last commit and discard changes (danger)

```bash
git reset --hard HEAD~1
```

## Reset Modes (What Changes?)

| Mode                | Moves `HEAD` / branch? | Updates Staging Area? | Updates Working Directory? |
| ------------------- | ---------------------: | --------------------: | -------------------------: |
| `--soft`            |                    Yes |                    No |                         No |
| `--mixed` (default) |                    Yes |                   Yes |                         No |
| `--hard`            |                    Yes |                   Yes |                        Yes |

## Pathspec Reset (Unstage Without Moving HEAD)

Reset can act like “unstage” when you provide paths:

```bash
# unstage a file (keep working changes)
git reset HEAD -- path/to/file

# unstage everything
git reset HEAD -- .
```

Modern alternative: [[git-restore]] with `--staged`.

## Recovery (If You Mess Up)

If you reset too far, use reflog:

```bash
git reflog
git reset --hard HEAD@{1}
```

See: [[git-reflog]]

## Common Workflows

### “I committed on the wrong branch” (local only)

```bash
# on wrong branch, undo commit but keep changes
git reset --soft HEAD~1

# switch to correct branch
git switch correct-branch

# recommit
git commit -m "Correct commit"
```

### “Split a big commit into smaller commits”

```bash
git reset --soft HEAD~1
git reset HEAD -- .          # unstage everything
git add part1
git commit -m "Part 1"
git add part2
git commit -m "Part 2"
```

## Troubleshooting

### Reset vs Revert?

- `reset` rewrites local history (best for private branches)
- `revert` preserves history with a new “undo” commit (best for shared branches)

## Related Commands

- [[git-revert]]
- [[git-reflog]]
- [[git-restore]]
- [[git-commit]]
