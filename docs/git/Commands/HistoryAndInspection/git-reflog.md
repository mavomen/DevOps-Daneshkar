---
id: git-reflog
aliases: []
tags: []
---

# git reflog

Show the local history of where references (especially `HEAD`) have pointed.

## Syntax

```bash
git reflog
git reflog show [<ref>]
git reflog --all
```

## Description

`git reflog` records movements of references like:

- `HEAD`
- branches (`main`, `feature/x`)
- sometimes other refs depending on operations

This is the go-to tool when you think you “lost commits” after operations like:

- `git reset`
- `git rebase`
- `git checkout` / `git switch`
- deleting a branch

Key idea: **`git log` shows commit history you can reach**, but **`git reflog` shows where your refs were**, even if the commits are currently unreachable from a branch.

## Basic Usage

### Show HEAD reflog

```bash
git reflog
```

### Show reflog for a specific branch

```bash
git reflog show main
```

### Show all reflogs

```bash
git reflog --all
```

## Understanding Reflog Entries

You’ll see entries like:

```txt
abc1234 HEAD@{0}: commit: Add feature
def5678 HEAD@{1}: rebase (finish): returning to refs/heads/main
...
```

Important notation:

- `HEAD@{0}` = where `HEAD` is now
- `HEAD@{1}` = one move ago
- `HEAD@{n}` = n moves ago

## Recovery Recipes

### Recover after an accidental reset (classic)

1. Find the previous state:

```bash
git reflog
```

2. Reset back:

```bash
git reset --hard HEAD@{1}
```

> If you’re not sure, create a safety branch first.

### Create a rescue branch (safe approach)

```bash
git reflog
git branch rescue/<name> <commit-or-HEAD@{n}>
```

Now the commit is reachable again via the rescue branch.

### Recover a deleted branch tip

```bash
git reflog --all
# find the commit hash that was the branch tip
git branch recovered-branch <commit-hash>
```

## Maintenance / Expiration

Reflogs are local and expire eventually (depending on config and GC).

You can inspect config:

```bash
git config --get gc.reflogExpire
git config --get gc.reflogExpireUnreachable
```

## Troubleshooting

### “I did a rebase and everything is weird”

- Use reflog to find `ORIG_HEAD`-like moments:

```bash
git reflog
git reset --hard HEAD@{n}
```

### “I force-pushed and now remote is different”

- Reflog helps locally, but remote recovery depends on remote state and server retention.
- First step is still: `git reflog` to find the commit you want.

## Related Notes

- [[git-reset]] - often the reason you need reflog
- [[git-rebase]] - can rewrite history; reflog helps recovery
- [[git-log]] - shows reachable history
- [[git-show]] - inspect candidate commits
