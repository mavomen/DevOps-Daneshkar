---
id: AdvancedCommands
aliases: []
tags: []
---

# Advanced Commands (Cheat Sheet)

Power tools: selective commit movement, temporary storage, tags, worktrees, and history rewrite.

## Selective / Advanced

```bash
git cherry-pick <commit>
git cherry-pick A^..B

git stash push -m "WIP"
git stash list
git stash pop
git stash apply stash@{0}
```

## Tags

```bash
git tag
git tag -a v1.0.0 -m "Release v1.0.0"
git show v1.0.0
git push origin --tags
```

## Worktrees

```bash
git worktree list
git worktree add <path> <branch>
git worktree remove <path>
git worktree prune
```

## Submodules

```bash
git submodule add <url> <path>
git submodule update --init --recursive
git submodule status
```

## History rewrite (danger zone)

```bash
git rebase -i
git reset --soft HEAD~1
git reset --hard HEAD~1
git filter-branch -- --all
```

## Related Notes

- [[git-cherry-pick]]
- [[git-stash]]
- [[git-tag]]
- [[git-worktree]]
- [[git-submodule]]
- [[git-filter-branch]]
- [[git-rebase]]
- [[git-reset]]
