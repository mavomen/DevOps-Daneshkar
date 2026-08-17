---
id: git-worktree
aliases: []
tags: []
---

# git worktree

Manage multiple working directories attached to the same Git repository.

## Syntax

```bash
git worktree list
git worktree add <path> [<commit-ish>]
git worktree remove <path>
git worktree prune
```

## Description

`git worktree` lets you check out multiple branches at once into separate directories without cloning again.

Good for:

- reviewing PRs while keeping your current branch open
- running builds/tests for multiple branches in parallel
- working on a hotfix without stashing your current work

## Basic Usage

### List existing worktrees

```bash
git worktree list
```

### Add a new worktree for a branch

```bash
git worktree add ../my-repo-hotfix hotfix/critical
```

### Add a new worktree for a new branch (common pattern)

```bash
git worktree add -b feature/new-ui ../my-repo-new-ui main
```

### Remove a worktree

```bash
git worktree remove ../my-repo-hotfix
```

## Options / Notes

- Each branch can generally be checked out in only one worktree at a time (Git will protect you from accidental dual checkouts).

## Troubleshooting

### “Branch is already checked out”

- Use a different branch, or detach, or remove the worktree where it’s checked out.

```bash
git worktree list
```

### Cleanup

If worktrees were removed manually at filesystem level:

```bash
git worktree prune
```

## Examples

```bash
# Keep main open while you work on a feature branch
git worktree add ../repo-main main
git worktree add -b feature/x ../repo-feature-x main
```


## Related Notes

- [[git-switch]] - normal single worktree switching
- [[git-stash]] - alternative approach if you don’t want multiple folders
- [[git-branch]] - create/manage branches
