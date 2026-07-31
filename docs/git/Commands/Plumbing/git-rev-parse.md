---
id: git-rev-parse
aliases: []
tags: []
---

# git rev-parse

Resolve “revision” names (refs, commit-ish) into raw object IDs, and query repo metadata.

## Syntax

```bash
git rev-parse <args>...
```

Common patterns:

```bash
git rev-parse HEAD
git rev-parse --verify <name>
git rev-parse --short <object>
git rev-parse --show-toplevel
git rev-parse --is-inside-work-tree
```

## Description

`git rev-parse` is a plumbing utility to translate human-friendly names into exact hashes and to answer “where am I?” questions about the repository.

It’s widely used in scripts.

Related concepts:

- [[HEAD]]
- [[SHAHash]]
- [[Repository]]

## Basic Usage

### Resolve HEAD (current commit hash)

```bash
git rev-parse HEAD
```

### Resolve a branch name

```bash
git rev-parse main
git rev-parse feature/my-branch
```

### Short hash

```bash
git rev-parse --short HEAD
git rev-parse --short=10 HEAD
```

### Verify a name exists

```bash
git rev-parse --verify HEAD
git rev-parse --verify refs/heads/main
```

If it doesn’t exist, it exits non-zero.

### Repo location queries

```bash
# absolute path to repo root
git rev-parse --show-toplevel

# is this directory inside a git work tree?
git rev-parse --is-inside-work-tree
```

## Useful Commit-ish Forms

```bash
git rev-parse HEAD~1
git rev-parse HEAD^
git rev-parse v1.0.0^{commit}
git rev-parse HEAD^{tree}
```

## Related Commands

- [[git-cat-file]] - inspect the object you resolved
- [[git-log]] / [[git-show]] - human-friendly history views
- [[git-update-ref]] - move refs (often uses hashes from rev-parse)
