---
id: git-fetch
aliases: []
tags: []
---

# git fetch

Download commits, branches, and tags from a remote **without** modifying your working directory or current branch.

## Syntax

```bash
git fetch [<remote>] [<refspec>...]
git fetch --all
git fetch --prune
git fetch --tags
```

## Description

`git fetch` updates your remote-tracking branches (like `origin/main`) by downloading new objects and refs from a remote. It is a safe way to “see what changed on the server” before integrating.

Fetch does **not**:

- merge
- rebase
- change your checked-out branch
- change your working directory

It only updates remote-tracking refs and object database.

Related concept: [[Concepts/Remote|Remote]]

## Basic Usage

### Fetch Default Remote

```bash
# Fetch from the default remote of the current branch (usually origin)
git fetch

# Fetch explicitly from origin
git fetch origin
```

### Fetch All Remotes

```bash
git fetch --all
```

### Fetch a Specific Branch

```bash
git fetch origin main
git fetch origin feature/my-branch
```

### Fetch + Prune

```bash
# Remove local references to remote branches deleted on the server
git fetch --prune
git fetch -p
```

### Fetch Tags

```bash
# Fetch tags reachable from fetched branches (common default behavior)
git fetch

# Fetch all tags explicitly
git fetch --tags
```

## What to Do After Fetch

### Inspect What Changed

```bash
# See commits on remote branch that you don't have locally
git log --oneline main..origin/main

# Show differences
git diff main..origin/main

# Visualize
git log --graph --oneline --decorate --all
```

### Integrate After Fetch

You typically integrate using either:

- merge: [[Commands/Branching/git-merge|git merge]]
- rebase: [[Commands/Branching/git-rebase|git rebase]]

Examples:

```bash
# Merge remote into current branch
git merge origin/main

# Rebase current branch onto remote branch
git rebase origin/main
```

## Common Workflows

### “Safe sync” workflow

```bash
git status
git fetch origin
git log --oneline --decorate --graph --all --max-count=30
# then choose merge or rebase
```

### Update local main from origin/main (merge style)

```bash
git switch main
git fetch origin
git merge origin/main
```

### Update local main from origin/main (rebase style)

```bash
git switch main
git fetch origin
git rebase origin/main
```

## Troubleshooting

### Fetch is slow

- Large repos: first fetch is expensive
- Consider:
  - pruning: `git fetch -p`
  - reducing work: fetch specific branch: `git fetch origin main`

### “Couldn't find remote ref …”

- The branch name may be wrong
- List remote branches after fetch:
  - `git branch -r`

## Related Notes

- [[Commands/Remote/git-remote|git remote]]
- [[Commands/Remote/git-pull|git pull]]
- [[Commands/Remote/git-push|git push]]
- [[Commands/BasicOperations/git-log|git log]]
- [[Commands/BasicOperations/git-diff|git diff]]
