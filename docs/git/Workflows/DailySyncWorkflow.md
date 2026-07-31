---
id: DailySyncWorkflow
aliases: []
tags: []
---

# Daily Sync Workflow

A repeatable “safe sync” routine for keeping your local branch aligned with the remote while minimizing surprises.

## Goal

- avoid accidental merge commits
- avoid losing local work
- make integration choice explicit (merge vs rebase)

## Recommended Routine

1. Check your state

```bash
git status
```

2. If you have WIP, either commit or stash

```bash
git stash push -m "WIP before sync"
```

3. Fetch remote changes (safe)

```bash
git fetch origin
```

4. Inspect what changed

```bash
git log --oneline --decorate --graph --all --max-count=30
git diff HEAD..origin/$(git branch --show-current)
```

5. Integrate (choose one)

### Merge (safe for shared branches)

```bash
git merge origin/$(git branch --show-current)
```

### Rebase (common for feature branches)

```bash
git rebase origin/$(git branch --show-current)
```

6. Push (if needed)

```bash
git push
```

7. Restore stashed work (if you stashed)

```bash
git stash pop
```

## Related Notes

- [[git-fetch]]
- [[git-pull]]
- [[git-rebase]]
- [[git-merge]]
- [[git-stash]]
- [[MergevsRebase]]
