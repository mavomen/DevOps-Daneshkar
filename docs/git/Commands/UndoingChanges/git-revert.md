---
id: git-revert
aliases: []
tags: []
---

# git revert

Create a new commit that undoes the changes introduced by an earlier commit.

## Syntax

```bash
git revert <commit>
git revert <commit>..<commit>
git revert --no-commit <commit>
```

## Description

`git revert` is a “safe undo” for shared history: it does **not** delete commits or rewrite history. Instead, it creates a new commit that applies the inverse patch of the commit you’re reverting.

This is usually preferred over [[git-reset]] on public branches.

## Basic Usage

### Revert one commit

```bash
git revert <commit-hash>
```

### Revert without committing immediately

This lets you batch multiple reverts into one commit or edit the result:

```bash
git revert --no-commit <commit-hash>
# then
git commit
```

### Revert a range

Revert commits reachable from the right side but not the left side:

```bash
git revert OLDEST^..NEWEST
```

Example:

```bash
git revert a1b2c3d^..f6e5d4c
```

## Reverting Merge Commits

A merge commit has multiple parents, so Git needs to know which parent is “mainline”.

```bash
git revert -m 1 <merge-commit-hash>
```

- `-m 1` means “treat parent 1 as mainline”
- Use `git show <merge-commit>^1` / `^2` to inspect parents if unsure (see [[git-show]])

## Common Workflows

### Undo a bad commit on main (shared branch)

```bash
git switch main
git pull
git revert <bad-commit>
git push
```

### Revert a feature quickly (if it was merged as a merge commit)

```bash
git revert -m 1 <merge-commit-hash>
```

## Conflicts

Reverts can conflict like merges.

Resolution is the standard flow:

```bash
git status
# fix files
git add .
git revert --continue
```

Abort:

```bash
git revert --abort
```

## Troubleshooting

### Revert vs Reset?

- Use `revert` when the commit is already shared/pushed
- Use `reset` for private branch cleanup before sharing

## Related Notes

- [[git-reset]]
- [[git-show]]
- [[git-log]]
- [[git-merge]]
