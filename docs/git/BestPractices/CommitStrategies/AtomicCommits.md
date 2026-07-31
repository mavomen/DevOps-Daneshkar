---
id: AtomicCommits
aliases: []
tags: []
---

# Atomic Commits

An atomic commit is a commit that represents **one logical change** and leaves the project in a consistent state.

## Why atomic commits matter

- easier code review (small, focused diffs)
- easier rollback (`git revert` can undo one change cleanly)
- easier debugging (`git bisect` works better)
- fewer conflicts during rebase/merge

Related:

- [[git-revert]]
- [[git-bisect]]
- [[MergevsRebase]]
- [[ConflictResolution]]

## Rules of thumb

- One intent per commit:
  - “Add endpoint X” (one commit)
  - “Refactor module Y” (one commit)
  - not both together
- Keep tests aligned:
  - include tests for the change in the same commit (or a clearly adjacent commit)
- Avoid mixing:
  - formatting-only changes with logic changes
  - unrelated files/areas in the same commit

## Techniques to create atomic commits

### Stage selectively

Use partial staging to split work:

```bash
git add -p
git commit -m "feat: add validation"
git add -p
git commit -m "fix: handle empty input"
```

### Unstage to re-split

If you staged too much:

```bash
git reset HEAD -- .
# then stage selectively again
git add -p
```

See: [[git-reset]]

### Split a too-big commit (local only)

```bash
git reset --soft HEAD~1
git reset HEAD -- .
# stage/commit in smaller units
git add -p
git commit -m "Part 1"
git add -p
git commit -m "Part 2"
```

## What “atomic” does NOT mean

- Not “one file per commit”
- Not “tiny commits that don’t compile”
- Not “never refactor” — refactor, but keep it isolated

## Related notes

- [[BestPractices/CommitStrategies/CommitFrequency|Commit Frequency]]
- [[git-add]]
- [[git-status]]
- [[git-diff]]
