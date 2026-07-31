---
id: git-hash-object
aliases: []
tags: []
---

# git hash-object

Compute the object ID (hash) of a file/content, and optionally write it into the object database.

## Syntax

```bash
git hash-object <file>...
git hash-object -w <file>...
git hash-object --stdin
git hash-object --stdin -w
```

## Description

`git hash-object` is plumbing for working with Git objects directly.

It can:

- compute the hash Git would use for content (usually a blob)
- optionally store the object in `.git/objects`

This is useful for understanding [[GitObjects]] and how [[SHAHash]] addresses content.

## Basic Usage

### Hash a file (do not write)

```bash
git hash-object path/to/file
```

### Hash and write object into database

```bash
git hash-object -w path/to/file
```

### Hash stdin (do not write)

```bash
printf "hello\n" | git hash-object --stdin
```

### Hash stdin and write

```bash
printf "hello\n" | git hash-object --stdin -w
```

## Options

### Specify object type

Most common is `blob` (default), but you can be explicit:

```bash
git hash-object -t blob path/to/file
```

## Notes / Gotchas

- Hashes are computed over a header + content, not just raw bytes, which is why Git hashes differ from hashing a file with `sha1sum`.
- Writing an object (`-w`) stores it, but it won’t be reachable from any commit unless you link it via trees/commits.

## Related Commands

- [[git-cat-file]] - inspect objects you wrote
- [[git-write-tree]] - build a tree from the index
- [[git-update-ref]] - update refs to point to commits (dangerous)
- [[GitObjects]]
