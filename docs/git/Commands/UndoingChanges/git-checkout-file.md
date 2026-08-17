---
id: git-checkout-file
aliases: []
tags: []
---

# git checkout (file)

Restore a file (or directory) from another commit/branch using the legacy `git checkout <ref> -- <path>` form.

## Syntax

```bash
git checkout <commit-ish> -- <pathspec>...
```

## Description

This note focuses only on the “checkout a file” use-case.

For branch switching and the broader behavior of `git checkout`, see [[git-checkout]].
For the modern recommended file-restore command, see [[git-restore]].

## Basic Usage

### Restore a file from HEAD (last commit)

```bash
git checkout HEAD -- path/to/file
```

### Restore a file from a previous commit

```bash
git checkout HEAD~1 -- path/to/file
git checkout <commit-hash> -- path/to/file
```

### Restore a file from another branch

```bash
git checkout main -- path/to/file
git checkout feature/branch -- path/to/file
```

### Restore a directory from another ref

```bash
git checkout <commit-ish> -- path/to/directory/
```

## Modern Equivalent (Recommended)

Everything above is usually better expressed as:

```bash
git restore --source=<commit-ish> -- path/to/file
```

Examples:

```bash
git restore --source=HEAD~1 -- path/to/file
git restore --source=main -- path/to/file
```

## Common Workflows

### “I broke one file; keep everything else”

```bash
git status
git checkout HEAD -- path/to/file
git status
```

### “Bring just one config file from main”

```bash
git checkout main -- config/app.yml
```

## Troubleshooting

### Pathspec confusion

Always include `--` to separate ref from paths:

```bash
git checkout HEAD -- --weird-filename.txt
```

## Related Notes

- [[git-checkout]]
- [[git-restore]]
- [[git-status]]
- [[git-diff]]
