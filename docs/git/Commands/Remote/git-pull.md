---
id: git-pull
aliases: []
tags: []
---

# git pull

Fetch from a remote and then integrate the fetched changes into the current branch (merge or rebase).

## Syntax

```bash
git pull [<options>] [<remote> [<branch>]]
```

## Description

`git pull` is effectively:

- `git fetch` + `git merge` (default), or
- `git fetch` + `git rebase` (if configured or requested)

It updates your current branch using new commits from the remote-tracking branch.

Related concepts:

- [[Concepts/Remote|Remote]]
- [[MergevsRebase|MergevsRebase]]

## Basic Usage

### Pull Current Branch (tracking upstream)

```bash
git pull
```

This works when your branch has an upstream configured (e.g., `main` tracking `origin/main`).

### Pull Explicit Remote + Branch

```bash
git pull origin main
git pull origin feature/my-branch
```

## Merge vs Rebase Pull

### Pull with Merge (default behavior)

```bash
git pull
# does: fetch + merge
```

### Pull with Rebase

```bash
git pull --rebase
git pull --rebase origin main
```

### Pull with Fast-Forward Only (no merge commit)

```bash
git pull --ff-only
```

## Common Workflows

### Start of day (safe-ish)

```bash
git status
git pull --ff-only
```

If it fails, it means your local branch diverged; then you choose merge or rebase intentionally.

### Keep feature branch updated

```bash
git switch feature/my-work
git pull --rebase origin main
```

(You are rebasing your feature work on top of the latest `main`.)

## Configuration

### Set default pull behavior

```bash
# Always rebase on pull (global)
git config --global pull.rebase true

# Always merge on pull (global)
git config --global pull.rebase false

# Only fast-forward on pull (global)
git config --global pull.ff only
```

## Troubleshooting

### Pull fails due to local changes

```bash
# Typical error:
# "Your local changes would be overwritten by merge"

# Options:
git stash
git pull
git stash pop
```

Or commit your work before pulling.

### Pull created an unexpected merge commit

- You likely had divergent history
- Use:
  - `git log --graph --oneline --decorate --all`
- Team policy may prefer `--rebase` or `--ff-only`

## Related Notes

- [[Commands/Remote/git-fetch|git fetch]]
- [[Commands/Branching/git-merge|git merge]]
- [[Commands/Branching/git-rebase|git rebase]]
- [[Commands/Remote/git-push|git push]]
