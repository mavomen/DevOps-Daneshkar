---
id: EmergencyRecovery
aliases: []
tags: []
---

# Emergency Recovery

A step-by-step recovery playbook when you think you lost work or broke history.

## Step 0: Stop making it worse

- Don’t run more destructive commands.
- Don’t `git gc` until you’ve recovered important commits.
- Copy the repo directory somewhere safe if you’re panicking.

## Step 1: Capture state (copy/paste into notes)

```bash
git status -sb
git log --oneline --decorate --graph --all -n 30
git reflog -n 30
git remote -v
git branch -vv
```

## Step 2: If you “lost commits” (most common)

Use reflog:

```bash
git reflog
```

Create a rescue branch at the last known good point:

```bash
git branch rescue/<name> HEAD@{1}
```

Or hard reset back (only if you’re sure):

```bash
git reset --hard HEAD@{1}
```

## Step 3: If you lost uncommitted changes

Check stashes:

```bash
git stash list
git stash show -p stash@{0}
git stash apply stash@{0}
```

If changes were never committed/stashed, recovery is not always possible.

## Step 4: If you deleted a branch

```bash
git reflog --all
git branch recovered <commit-hash>
```

## Step 5: If the repo feels corrupted

- First: reclone (best)
- If you must inspect:

```bash
git fsck --full
```

## Step 6: Validate the recovery

```bash
git log --oneline -n 20
git status
```

## Related Notes

- [[git-reflog]]
- [[LostCommits|LostCommits]]
- [[Troubleshooting/CommonProblems/CorruptedRepository|CorruptedRepository]]
- [[Troubleshooting/RecoveryScenarios/RecoverDeletedBranch|RecoverDeletedBranch]]
