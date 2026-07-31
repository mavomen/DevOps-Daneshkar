---
id: GitAliases
aliases: []
tags: []
---

# Git Aliases

Define short names for common Git commands to speed up your workflow.

## Suggested Aliases (optional)

- `Git Aliases`

## Basic Alias Setup

Aliases are stored in Git config:

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.sw switch
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.df diff
git config --global alias.lg "log --oneline --graph --decorate --all"
```

Use them:

```bash
git st
git lg
git co main
```

## Practical Aliases (Recommended)

### Status / Log

```bash
git config --global alias.s "status --short --branch"
git config --global alias.l "log --oneline --decorate"
git config --global alias.graph "log --graph --oneline --decorate --all"
```

### Undo helpers (safe)

```bash
git config --global alias.unstage "restore --staged"
git config --global alias.discard "restore"
```

### Update helpers

```bash
git config --global alias.up "pull --ff-only"
git config --global alias.f "fetch --prune"
```

## Advanced Aliases (Shell Functions)

Git aliases can run shell via `!`:

```bash
git config --global alias.wip '!f(){ git add -A && git commit -m "WIP"; }; f'
```

## Manage / Inspect

```bash
git config --global --get-regexp ^alias\.
git config --global --edit
```

## Related Notes

- [[GitConfiguration]]
- [[ShellIntegration]]
- [[git-config]]
