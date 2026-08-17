---
id: git-push
aliases: []
tags: []
---

# git push

Upload local commits (and refs like branches/tags) to a remote repository.

## Syntax

```bash
git push [<options>] [<remote>] [<refspec>...]
```

## Description

`git push` transfers commits and updates remote references (branches/tags). You typically push the current branch to its upstream (e.g., local `main` → `origin/main`).

Related concept: [[Concepts/Remote|Remote]]

## Basic Usage

### Push Current Branch (with upstream set)

```bash
git push
```

### Push Explicit Remote + Branch

```bash
git push origin main
git push origin feature/my-branch
```

### Set Upstream on First Push

```bash
git push -u origin feature/my-branch
```

This sets the tracking relationship so future `git push`/`git pull` can omit remote/branch.

## Push Variants

### Push a Local Branch to a Different Remote Branch Name

```bash
git push origin local-branch:remote-branch
```

### Delete a Remote Branch

```bash
git push origin --delete feature/old-branch

# Equivalent older syntax
git push origin :feature/old-branch
```

### Push Tags

```bash
# Push a single tag
git push origin v1.0.0

# Push all tags
git push origin --tags
```

## Force Push (Danger Zone)

### Force

```bash
git push --force origin feature/my-branch
```

This can overwrite remote history and delete commits others might have based work on.

### Safer Force: --force-with-lease

```bash
git push --force-with-lease origin feature/my-branch
```

This refuses to overwrite if the remote moved since you last fetched.

## Common Workflows

### Feature branch push

```bash
git switch -c feature/new-work
# ... commits ...
git push -u origin feature/new-work
```

### After interactive rebase (history rewrite)

```bash
# you rebased local feature branch
git push --force-with-lease origin feature/my-branch
```

## Troubleshooting

### “rejected: non-fast-forward”

Means the remote has commits you don’t have locally, or you rewrote history locally.

Typical fixes:

```bash
# Option 1: integrate remote changes, then push
git pull --rebase
git push

# Option 2: if you intentionally rewrote history (feature branch)
git fetch origin
git push --force-with-lease origin feature/my-branch
```

### “failed to push some refs”

- Check which branch you’re on: `git status`
- Check upstream: `git branch -vv`
- Verify remote exists: `git remote -v`

## Related Notes

- [[Commands/Remote/git-remote|git remote]]
- [[Commands/Remote/git-fetch|git fetch]]
- [[Commands/Remote/git-pull|git pull]]
- [[Commands/BasicOperations/git-log|git log]]
- [[Commands/Branching/git-rebase|git rebase]]
