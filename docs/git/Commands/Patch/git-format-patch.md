---
id: git-format-patch
aliases: []
tags: []
---

# git format-patch

Export commits as email-style patch files (mbox format) that can be applied with [[git-am]].

## Syntax

```bash
git format-patch [<options>] <since>..<until>
git format-patch [<options>] -n <since>..<until>
git format-patch [<options>] <since>
```

## Description

`git format-patch` creates patch files that include:

- commit diffs
- commit messages
- author info
- commit metadata

These patches are designed to be applied with:

- [[git-am]] (preserves author/message and creates commits)

If you want a plain patch without metadata, use `git diff > file.patch` and apply with [[git-apply]].

## Basic Usage

### Export last N commits

```bash
git format-patch -1            # last 1 commit
git format-patch -3            # last 3 commits
```

### Export a commit range

```bash
git format-patch A^..B
```

### Export all commits since a base

```bash
git format-patch main..HEAD
```

## Output Location

By default, patches are created in the current directory as:

- `0001-*.patch`
- `0002-*.patch`
- ...

### Choose output directory

```bash
git format-patch -o /tmp/patches -3
```

## Useful Options

### Include a cover letter (for patch series)

```bash
git format-patch --cover-letter -o /tmp/patches main..HEAD
```

### Keep subject prefix (common)

```bash
git format-patch --subject-prefix="PATCH" -o /tmp/patches -3
```

### Add base information (helps reviewers)

```bash
git format-patch --base=auto -o /tmp/patches main..HEAD
```

## Applying patches (typical)

In target repo:

```bash
git am /tmp/patches/*.patch
```

## Troubleshooting

### “I only need the diff, not commits”

Use `git diff`:

```bash
git diff main..HEAD > changes.patch
```

Then apply with:

```bash
git apply changes.patch
```

### Patches don’t apply cleanly

- ensure target repo is based on the expected commit/base
- use `git am --abort` if needed
- resolve conflicts and `git am --continue`

## Related Commands

- [[git-am]]
- [[git-apply]]
- [[git-diff]]
- [[git-log]]
