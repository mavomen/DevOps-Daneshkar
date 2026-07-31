---
id: git-add
aliases: []
tags: []
---

# git add

Add file contents to the staging area (index).

## Syntax

```bash
git add <path>...
git add .
git add -p
```

## Description

`git add` updates the [[StagingArea]] to match chosen content from your [[WorkingDirectory]].

## Common usage

### Stage a file or directory

```bash
git add README.md
git add src/
```

### Stage everything under current directory

```bash
git add .
```

### Stage interactively (recommended for atomic commits)

```bash
git add -p
```

## Tips

- Review what you staged:

```bash
git diff --staged
```

## Related Notes

- [[StagingArea]]
- [[AtomicCommits]]
- [[git-status]]
- [[git-commit]]
