---
id: RecoverDeletedBranch
aliases: []
tags: []
---

# Recover Deleted Branch

If a branch was deleted, its commits might still exist and be recoverable via reflog.

## Recovery steps

1. Search reflog:

```bash
git reflog --all
```

2. Find the commit hash that was the branch tip.

3. Recreate branch:

```bash
git branch recovered-branch <commit-hash>
```

4. Verify:

```bash
git log --oneline -n 20 recovered-branch
```

## Related Notes

- [[git-reflog]]
- [[LostCommits]]
