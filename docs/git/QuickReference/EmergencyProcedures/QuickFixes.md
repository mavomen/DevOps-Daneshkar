---
id: QuickFixes
aliases: []
tags: []
---

# Quick Fixes

Fast “do this now” commands for common Git emergencies.

## Always start with

```bash
git status -sb
git log --oneline -n 20
```

## I staged the wrong files

```bash
git restore --staged <file>
# or unstage everything
git restore --staged .
```

Then stage correctly:

```bash
git add -p
```

## I edited a file and want to discard changes

```bash
git restore <file>
# discard all local working changes (careful)
git restore .
```

## I committed with the wrong message (local only)

```bash
git commit --amend
```

If already pushed, coordinate (history rewrite).

## I need to undo the last commit

- Keep changes (recommended):

```bash
git reset --soft HEAD~1
```

- Discard changes (danger):

```bash
git reset --hard HEAD~1
```

## I committed on the wrong branch (local)

```bash
# on wrong branch
git reset --soft HEAD~1
git switch <correct-branch>
git commit -m "Correct commit"
```

Alternative (if already committed and you want to move it):

```bash
git switch <correct-branch>
git cherry-pick <commit>
```

## Push rejected (non-fast-forward)

```bash
git fetch --prune
git pull --rebase
git push
```

If you intentionally rewrote history (feature branch only):

```bash
git push --force-with-lease
```

## Merge conflict happened

```bash
git status
# fix files
git add .
git commit
```

Or abort:

```bash
git merge --abort
```

## Rebase conflict happened

```bash
git status
# fix files
git add .
git rebase --continue
```

Or abort:

```bash
git rebase --abort
```

## Related Notes

- [[ConflictResolution]]
- [[git-reset]]
- [[git-revert]]
- [[git-reflog]]
- [[MergeConflicts|MergeConflicts]]
