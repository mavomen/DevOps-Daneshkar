---
id: BranchingCommands
aliases: []
tags: []
---

# Branching Commands (Cheat Sheet)

Commands for creating, switching, integrating, and cleaning up branches.

## Create / List / Delete

```bash
git branch
git branch -a
git branch -vv

git branch <name>
git branch -d <name>
git branch -D <name>
```

## Switch

```bash
git switch <name>
git switch -c <name>
git switch -
```

Legacy:

```bash
git checkout <name>
git checkout -b <name>
```

## Merge / Rebase

```bash
git merge <branch>
git merge --no-ff <branch>
git merge --ff-only <branch>

git rebase <upstream>
git rebase -i <upstream>
git rebase --continue
git rebase --abort
```

## Compare branches

```bash
git log main..feature --oneline
git log main...feature --oneline --left-right

git diff main..feature
git diff main...feature
```

## Cleanup remote branches

```bash
git fetch --prune
git push origin --delete <branch>
```

## Related Notes

- [[git-branch]]
- [[git-switch]]
- [[git-checkout]]
- [[git-merge]]
- [[git-rebase]]
- [[MergevsRebase]]
