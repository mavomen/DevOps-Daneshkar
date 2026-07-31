---
id: LostCommits
aliases: []
tags: []
---

# Lost Commits

“Lost commits” usually means commits are not reachable from your current branch, not that they are gone forever.

## Common causes

- `git reset` moved branch pointer back
- `git rebase` rewrote history
- branch was deleted
- commits were made in detached HEAD

## Fast Diagnosis

```bash
git log --oneline -n 30
git reflog -n 50
```

## Recovery (most common)

### Create a rescue branch from reflog

```bash
git reflog
git branch rescue/<name> HEAD@{n}
```

### Reset back (if that’s what you want)

```bash
git reset --hard HEAD@{n}
```

## If the commits were pushed and then overwritten

- recovery depends on remote retention and whether anyone else has the commits.
- check teammates’ clones or remote UI (if available).

## Related Notes

- [[git-reflog]]
- [[git-reset]]
- [[git-rebase]]
- [[Troubleshooting/RecoveryScenarios/RecoverDeletedBranch|RecoverDeletedBranch]]
