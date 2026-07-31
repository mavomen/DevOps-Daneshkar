---
id: RecoverLostChanges
aliases: []
tags: []
---

# Recover Lost Changes

Playbook for recovering work after resets, rebases, branch deletes, or accidental discards.

## If changes were committed

Use reflog:

```bash
git reflog
```

Then rescue:

```bash
git branch rescue/<name> HEAD@{n}
```

## If changes were stashed

```bash
git stash list
git stash show -p stash@{0}
git stash apply stash@{0}
```

## If changes were staged but not committed

Try to avoid losing them; if you already ran commands that discarded index/worktree, recovery may not be possible.

## If you discarded working changes

If you used `git restore .` or `git reset --hard`, recovery is difficult.
Check reflog anyway (sometimes you actually had commits):

```bash
git reflog
```

## Related Notes

- [[git-reflog]]
- [[git-stash]]
- [[LostCommits|LostCommits]]
