---
id: DetachedHead
aliases: []
tags: []
---

# Detached HEAD

Detached HEAD means `HEAD` points directly to a commit (not to a branch).

## Symptoms

- `git status` says: “You are in 'detached HEAD' state”
- you checked out a commit hash or tag

Example causes:

```bash
git checkout <commit>
git checkout v1.0.0
git switch --detach <commit>
```

## Why it matters

You can commit, but those commits won’t belong to a named branch unless you create one. They can become hard to find later.

## Fix: keep the work

If you made commits you want to keep:

```bash
git switch -c rescue/my-work
```

## Fix: return to normal

```bash
git switch main
```

## Recovery if you “lost” detached commits

Use reflog:

```bash
git reflog
git branch recovered <commit-hash>
```

## Related Notes

- [[HEAD]]
- [[git-reflog]]
- [[git-switch]]
- [[LostCommits|LostCommits]]
