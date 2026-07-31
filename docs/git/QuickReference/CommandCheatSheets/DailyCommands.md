---
id: DailyCommands
aliases: []
tags: []
---

# Daily Commands (Cheat Sheet)

Most-used Git commands for everyday work.

## Status / Inspect

```bash
git status
git status -sb

git diff
git diff --staged

git log --oneline -n 20
git log --graph --oneline --decorate --all
git show HEAD
```

## Stage / Commit

```bash
git add <file>
git add .
git add -p

git commit -m "message"
git commit --amend
```

## Undo (common)

```bash
git restore <file>
git restore --staged <file>

git rm <file>
git rm --cached <file>

git clean -n
git clean -fd
```

## Sync (common)

```bash
git fetch --prune
git pull
git pull --rebase
git push
git push -u origin <branch>
```

## Quick “safe loop”

```bash
git status
git diff
git add -p
git commit -m "..."
git fetch --prune
git pull --rebase
git push
```

## Related Notes

- [[git-status]]
- [[git-diff]]
- [[git-add]]
- [[git-commit]]
- [[git-restore]]
- [[git-fetch]]
- [[git-pull]]
- [[git-push]]
