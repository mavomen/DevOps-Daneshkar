---
id: git-mv
aliases: []
tags: []
---

# git mv

Move or rename a file (or directory) and stage the change for commit.

## Syntax

```bash
git mv [<options>] <source>... <destination>
```

## Description

`git mv` is a convenience command that combines:

- renaming/moving paths in your working directory, and
- staging that rename/move in the index

It’s roughly equivalent to:

```bash
mv <source> <destination>
git add <destination>
git rm <source>
```

But `git mv` is simpler and reduces chances of mistakes.

## Basic Usage

### Rename a file

```bash
git mv oldname.txt newname.txt
git status
git commit -m "Rename oldname.txt to newname.txt"
```

### Move a file into a directory

```bash
git mv README.md docs/README.md
git commit -m "Move README into docs/"
```

### Move/rename a directory

```bash
git mv src/ legacy-src/
git commit -m "Rename src to legacy-src"
```

## Options / Notes

### Force overwrite destination (careful)

```bash
git mv -f a.txt b.txt
```

### Renames and Git

Even if you don’t use `git mv`, Git can often _detect_ renames during commits/merges by similarity, but:

- using `git mv` makes intent explicit
- it avoids staging mistakes and keeps index consistent

## Common Workflows

### Fix wrong path name before commit

```bash
git status
git mv typo-fielname.js correct-filename.js
git commit -m "fix: correct filename typo"
```

### Rename case only (macOS/Windows case-insensitive FS)

Sometimes case-only renames are tricky. A safe pattern:

```bash
git mv File.txt file_tmp.txt
git mv file_tmp.txt file.txt
git commit -m "chore: normalize filename case"
```

## Troubleshooting

### “destination exists”

- choose a new name, or delete/move the destination first
- or use `-f` only if you really want to overwrite

### “not under version control”

`git mv` works best for tracked paths. If it’s untracked, just move it and then `git add`.

## Related Commands

- [[git-add]]
- [[git-rm]]
- [[git-status]]
- [[git-commit]]
