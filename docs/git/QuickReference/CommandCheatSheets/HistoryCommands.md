---
id: HistoryCommands
aliases: []
tags: []
---

# History Commands (Cheat Sheet)

Find what happened, when it happened, and who did it.

## Log / Show

```bash
git log
git log --oneline -n 20
git log --graph --oneline --decorate --all

git show
git show <commit>
git show <commit> -- <path>
```

## Diff

```bash
git diff
git diff --staged
git diff <commit1> <commit2>
git diff <branch1>..<branch2>
git diff <branch1>...<branch2>
```

## Blame

```bash
git blame <file>
git blame -L 10,40 <file>
git blame -w <file>
```

## Reflog (recovery)

```bash
git reflog
git reflog show main
git reset --hard HEAD@{1}
```

## Bisect (find bug-introducing commit)

```bash
git bisect start
git bisect bad HEAD
git bisect good <good-commit-or-tag>
# test each checked-out commit
git bisect good
git bisect bad
git bisect reset
```

## Related Notes

- [[git-log]]
- [[git-show]]
- [[git-diff]]
- [[git-blame]]
- [[git-reflog]]
- [[git-bisect]]
