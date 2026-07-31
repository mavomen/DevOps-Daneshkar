---
id: MergeConflicts
aliases: []
tags: []
---

# Merge Conflicts

A merge conflict occurs when Git cannot automatically combine changes from two histories.

## Symptoms

- `git merge` stops and reports conflicts
- files contain conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
- `git status` shows “unmerged paths”

## Fast Diagnosis

```bash
git status
git diff
```

## Fix (standard flow)

1. Edit conflicted files, remove markers, choose correct content.
2. Stage resolved files:

```bash
git add <file>
# or
git add .
```

3. Finish merge:

```bash
git commit
# or
git merge --continue
```

## Abort merge

```bash
git merge --abort
```

## Helpful tools

- In-file helpers (merge):

```bash
git checkout --ours <file>
git checkout --theirs <file>
```

- Visual tool:

```bash
git mergetool
```

## Prevention

- integrate frequently (don’t let branches diverge too long)
- keep commits small and focused (see [[AtomicCommits]])
- coordinate on hot files

## Related Notes

- [[ConflictResolution]]
- [[ThreeWayMerge]]
- [[git-merge]]
- [[git-status]]
