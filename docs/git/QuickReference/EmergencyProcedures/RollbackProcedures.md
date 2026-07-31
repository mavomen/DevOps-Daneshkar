---
id: RollbackProcedure
aliases: []
tags: []
---

# Rollback Procedures

How to roll back changes safely (especially on shared branches like `main`).

## Principle: prefer revert over reset

- Shared branch rollback: use [[git-revert]]
- Local/private cleanup: [[git-reset]] is fine

## Roll back a single commit on main

```bash
git switch main
git pull --ff-only
git revert <bad-commit>
git push
```

## Roll back multiple commits (range)

```bash
# revert NEWEST..OLDEST (careful with order)
git revert OLDEST^..NEWEST
git push
```

## Roll back a merged feature (merge commit)

If the feature was merged with a merge commit:

```bash
git revert -m 1 <merge-commit>
git push
```

## Roll back by deploying an older tag (release workflow)

If your deployment system supports “deploy tag”:

- identify last known good tag:

```bash
git tag
git show vX.Y.Z
```

Then deploy that tag in your CD system.

## If you must reset (rare on shared branches)

Only when you control the branch and team coordination is perfect:

```bash
git reset --hard <good-commit>
git push --force-with-lease
```

## Related Notes

- [[git-revert]]
- [[git-reset]]
- [[git-push]]
- [[git-show]]
- [[Workflows/ReleaseWorkflow|ReleaseWorkflow]]
