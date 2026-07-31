---
id: ResetToPreviousState
aliases: []
tags: []
---

# Reset to Previous State

Return your branch (and optionally your working tree) to an earlier commit.

## Choose the right tool

- Shared branch rollback: [[git-revert]]
- Local/private rollback: [[git-reset]]
- Recover “where I used to be”: [[git-reflog]]

## Local reset (private branch)

### Move branch pointer and keep changes staged

```bash
git reset --soft <commit>
```

### Move branch pointer and keep changes in working tree (unstaged)

```bash
git reset <commit>
```

### Move branch pointer and discard changes (danger)

```bash
git reset --hard <commit>
```

## If you don’t know which commit

Use reflog:

```bash
git reflog
git reset --hard HEAD@{n}
```

## Related Notes

- [[git-reset]]
- [[git-reflog]]
