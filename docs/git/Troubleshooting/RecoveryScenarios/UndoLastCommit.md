---
id: UndoLastCommit
aliases: []
tags: []
---

# Undo Last Commit

Choose the correct undo method depending on whether the commit was pushed/shared.

## Case A: Local commit, not pushed

### Keep changes staged

```bash
git reset --soft HEAD~1
```

### Keep changes but unstage

```bash
git reset HEAD~1
```

### Discard everything (danger)

```bash
git reset --hard HEAD~1
```

## Case B: Commit already pushed/shared

Use revert:

```bash
git revert HEAD
git push
```

## Related Notes

- [[git-reset]]
- [[git-revert]]
- [[RollbackProcedures]]
