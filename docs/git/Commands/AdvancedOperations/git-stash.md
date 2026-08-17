---
id: git-stash
aliases: []
tags: []
---

# git stash

Temporarily save working directory changes (tracked files) and revert to a clean state.

## Syntax

```bash
git stash
git stash push [-m <message>] [-- <pathspec>...]
git stash list
git stash show [<stash>]
git stash pop [<stash>]
git stash apply [<stash>]
git stash drop [<stash>]
git stash clear
```

````

## Description

`git stash` is a stack of “work in progress” snapshots. It’s useful when you need to switch branches but you’re not ready to commit.

Typical uses:

- context switching (urgent fix on another branch)
- pulling/rebasing with a clean working tree
- parking experimental changes temporarily

## Basic Usage

### Stash current changes

```bash
git stash
# equivalent-ish to: git stash push
```

### Stash with a message

```bash
git stash push -m "WIP: refactor auth flow"
```

### List stashes

```bash
git stash list
```

### Inspect a stash

```bash
git stash show stash@{0}
git stash show -p stash@{0}
```

### Re-apply stash (and remove it)

```bash
git stash pop
# or explicit:
git stash pop stash@{0}
```

### Apply stash (keep it in the stash stack)

```bash
git stash apply stash@{0}
```

## Options

### Stash only some paths

```bash
git stash push -m "stash only docs" -- docs/
```

### Include untracked files

```bash
git stash -u
git stash push -u -m "WIP including untracked"
```

## Troubleshooting

### Conflicts when applying/popping

Applying a stash can conflict like a merge:

1. resolve conflicts
2. `git add ...`
3. commit or continue working

See: [[ConflictResolution]]

### “Stash didn’t include my untracked files”

Default stash excludes untracked files. Use `-u`.

## Examples

```bash
# Quick context switch to another branch
git stash push -m "WIP before hotfix"
git switch hotfix/critical
# ...
git switch -
git stash pop
````


## Related Notes

- [[git-switch]] / [[git-checkout]] - context switching
- [[git-clean]] - remove untracked junk (different problem)
- [[git-commit]] - make a real checkpoint instead of stashing
