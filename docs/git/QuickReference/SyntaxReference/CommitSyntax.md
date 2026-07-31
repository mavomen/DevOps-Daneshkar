---
id: CommitSyntax
aliases: []
tags: []
---

# Commit Syntax

How to refer to commits and ranges, and how to build commit messages consistently.

## Commit references (commit-ish)

Examples of commit-ish:

- `HEAD`
- `HEAD~1`, `HEAD~2`
- `HEAD^` (first parent)
- `HEAD^2` (second parent of a merge)
- branch names: `main`, `feature/x`
- tags: `v1.0.0`
- SHA: `1a2b3c4` (abbrev) / full hash

Examples:

```bash
git show HEAD
git show HEAD~3
git show main
git show v1.0.0
git show 1a2b3c4
```

## Parent / ancestor operators

- `~n` = n steps following first-parent chain
- `^` = parent selector

```bash
HEAD~1    # previous commit (first-parent)
HEAD^     # same as HEAD^1
HEAD^2    # second parent (merge commits)
```

## Range syntax

### Double-dot: `A..B`

“Commits reachable from `B` but not from `A`”

```bash
git log A..B --oneline
```

### Triple-dot: `A...B`

“Commits reachable from either side but not both” (symmetric difference)

```bash
git log A...B --oneline --left-right
```

## Commit message structure (recommended)

```txt
type(scope): summary

Why:
- ...

What:
- ...

Refs:
- ...
```

See: [[CommitMessageBestPractices]]
