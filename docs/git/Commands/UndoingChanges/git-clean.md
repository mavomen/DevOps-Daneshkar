---
id: git-clean
aliases: []
tags: []
---

# git clean

Remove untracked files (and optionally directories) from the working directory.

## Syntax

```bash
git clean [<options>]
```

## Description

`git clean` deletes files that are **not tracked by Git** (untracked). This is commonly used to clean build artifacts, generated files, and leftover junk.

It can be destructive—always preview first.

## Basic Usage

### Preview (Dry Run)

```bash
git clean -n
# shows what would be removed
```

### Remove untracked files (requires force)

```bash
git clean -f
```

### Remove untracked files and directories

```bash
git clean -fd
```

## Include / Exclude Ignored Files

### Remove ignored + untracked

```bash
git clean -fdx
```

### Remove only ignored files (keep untracked non-ignored)

```bash
git clean -fdX
```

## Interactive Clean

```bash
git clean -i
```

This lets you select what to delete.

## Common Workflows

### “Reset repo to a clean working tree” (without touching commits)

```bash
git status
git clean -nd   # preview
git clean -fd   # delete untracked junk
```

### After switching branches (build artifacts conflict)

```bash
git clean -fd
```

## Safety Notes

- `git clean` does **not** remove tracked files (use [[git-restore]] / [[git-reset]] / [[git-rm]] for tracked)
- `-x` can delete valuable ignored files (like `.env`) if they are ignored—use with care

## Troubleshooting

### “git clean did nothing”

- Your files might be tracked (check `git status`)
- Or they might not match options (e.g., directories require `-d`)

## Related Commands

- [[git-status]]
- [[git-restore]]
- [[git-reset]]
- [[git-rm]]

````

---

## `Commands/UndoingChanges/git-checkout-file.md`

```md
# git checkout (file)

Restore a file (or directory) from another commit/branch using the legacy `git checkout <ref> -- <path>` form.

## Syntax

```bash
git checkout <commit-ish> -- <pathspec>...
````

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

## Related Commands

- [[git-checkout]]
- [[git-restore]]
- [[git-status]]
- [[git-diff]]
