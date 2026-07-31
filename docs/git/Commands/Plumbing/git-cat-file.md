---
id: git-cat-file
aliases: []
tags: []
---

# git cat-file

Inspect Git objects (commits, trees, blobs, tags) by type, size, or content.

## Syntax

```bash
git cat-file -t <object>
git cat-file -s <object>
git cat-file -p <object>
git cat-file -e <object>

# batch modes (for scripts)
git cat-file --batch
git cat-file --batch-check
```

## Description

`git cat-file` is a Git _plumbing_ command used to inspect objects stored in the object database (`.git/objects` and packfiles).

It’s the fastest way to answer:

- “What type of object is this SHA?”
- “What’s inside this commit/tree/blob/tag object?”
- “Does this object exist locally?”

Related concepts:

- [[GitObjects]]
- [[SHAHash]]
- [[Repository]]

## Basic Usage

### Show object type

```bash
git cat-file -t <object>
# outputs: commit | tree | blob | tag
```

### Show object size (bytes)

```bash
git cat-file -s <object>
```

### Pretty-print object content

```bash
git cat-file -p <object>
```

Examples:

```bash
git cat-file -p HEAD          # commit content
git cat-file -p HEAD^{tree}   # tree listing for HEAD
git cat-file -p HEAD:README.md  # blob content (file content)
```

### Check existence (no output)

```bash
git cat-file -e <object>
# exit code 0 if exists, non-zero if not
```

## Object Specifiers (“object” argument)

Common forms you can pass:

- commit-ish: `HEAD`, `HEAD~2`, `<commit-hash>`, `main`
- peel operators:
  - `v1.0.0^{commit}` (resolve tag to commit)
  - `HEAD^{tree}` (commit → tree)
- path lookup: `HEAD:path/to/file` (tree lookup → blob)

## Batch Modes (Scripting)

### `--batch`

Read object IDs from stdin and print their contents:

```bash
printf "HEAD\nHEAD^{tree}\n" | git cat-file --batch
```

### `--batch-check`

Only print metadata (type/size), not full content:

```bash
printf "HEAD\nHEAD^{tree}\n" | git cat-file --batch-check
```

Useful when you need to inspect many objects efficiently.

## Troubleshooting

### “bad object …”

- the object isn’t in your local DB
- fetch it (if it’s on a remote) and try again:
  - `git fetch`
- or you mistyped the hash/ref

## Related Commands

- [[git-rev-parse]] - resolve names to object IDs
- [[git-hash-object]] - create blob objects from content
- [[git-write-tree]] - write a tree object from the index
- [[git-commit-tree]] - create commits from trees
