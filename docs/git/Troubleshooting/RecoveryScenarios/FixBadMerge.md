---
id: FixBadMerge
aliases: []
tags: []
---

# Fix Bad Merge

You merged something and the result is wrong.

## Case A: Merge commit not pushed (simple)

Reset branch back one commit:

```bash
git reset --hard HEAD~1
```

> This removes the merge commit locally.

## Case B: Merge commit already pushed/shared (safe)

Revert the merge commit:

```bash
git revert -m 1 <merge-commit-hash>
git push
```

## Find the merge commit hash

```bash
git log --oneline --merges -n 10
git show <merge-commit-hash>
```

## Related Notes

- [[git-reset]]
- [[git-revert]]
- [[git-merge]]
- [[RollbackProcedures]]
