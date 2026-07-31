---
id: git-ls-tree
aliases: []
tags: []
---

# git ls-tree

List the contents of a tree object (a directory snapshot) from a commit/tree-ish.

## Syntax

```bash
git ls-tree [<options>] <tree-ish> [--] [<path>...]
```

## Description

`git ls-tree` is a plumbing command that prints entries in a tree:

- files (blobs)
- subdirectories (trees)
- optionally submodules (commit entries)

It’s useful for inspecting repository state without checking it out.

Related concepts:

- [[GitObjects]]
- [[Repository]]
- [[git-cat-file]]

## Common Usage

### List top-level entries of `HEAD`

```bash
git ls-tree HEAD
```

### List recursively

```bash
git ls-tree -r HEAD
```

### Names only (no modes/hashes)

```bash
git ls-tree --name-only HEAD
git ls-tree -r --name-only HEAD
```

### Long format (include object sizes for blobs)

```bash
git ls-tree -l HEAD
```

### Inspect a subdirectory within a commit

```bash
git ls-tree HEAD -- src/
git ls-tree -r HEAD -- src/
```

### Inspect a specific tree-ish

```bash
git ls-tree main
git ls-tree <commit-hash>
git ls-tree <tree-hash>
```

## Output Format (default)

Typical line:

```txt
<mode> <type> <object>    <file>
```

Example:

```txt
100644 blob a1b2c3d4e5f6...    README.md
040000 tree deadbeefcafe...    src
```

## Useful Options

- `-r`: recurse into subtrees
- `-d`: show only tree entries (directories)
- `-t`: show tree entries even in recursive mode
- `-l`: include blob sizes
- `--name-only`: print file names only
- `-z`: NUL-terminate entries (scripts)

Example (directories only):

```bash
git ls-tree -d HEAD
```

## Related Notes

- [[git-cat-file]]
- [[git-rev-parse]]
- [[GitObjects]]
