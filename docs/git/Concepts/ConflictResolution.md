---
id: ConflictResolution
aliases: []
tags: []
---

# Conflict Resolution

Conflict resolution is the process of manually deciding how to combine two incompatible changes when Git can’t automatically merge or rebase them.

## What is a Conflict?

A conflict happens when Git tries to combine changes from two different histories (typically via [[git-merge]] or [[git-rebase]]), but both sides changed the same “hunk” in a way Git can’t reconcile.

Common scenarios:

- Two branches edited the same lines differently
- One branch deleted a file while the other modified it
- Both branches added a file with the same path but different content

Related concepts:

- [[ThreeWayMerge]]
- [[MergevsRebase]]
- [[GitHistory]]
- [[HEAD]]
- [[SHAHash]]

## How Conflicts Look (Markers)

Git writes conflict markers into the file:

```txt
<<<<<<< HEAD
# our version (the branch you are on)
=======
# their version (the branch being merged/rebased in)
>>>>>>> feature-branch
```

Your job is to:

1. Remove the markers
2. Produce the correct final content
3. Tell Git “this is resolved” by staging the fixed file

## “Ours” vs “Theirs”

### In a merge conflict

- **Ours** = current branch (you are merging _into_)
- **Theirs** = branch you are merging _from_

Example:

```bash
git switch main
git merge feature-x
# ours   = main
# theirs = feature-x
```

### In a rebase conflict

During a rebase, the meaning feels flipped depending on the step, because commits are being replayed.
Practical rule:

- Trust `git status` to tell you what’s happening
- Use tooling (diff/mergetool/editor) to pick the correct final content
- Finish with `git rebase --continue`

## Conflict Resolution Checklist

### 1) Confirm you’re in a conflict

```bash
git status
```

### 2) See the conflict hunks

```bash
git diff
```

### 3) Resolve the file(s)

- Edit files manually (remove markers, keep correct content)
- Or use your editor’s merge UI / `git mergetool`

Optional helpers:

```bash
# In a merge: pick one side entirely for a file
git checkout --ours path/to/file
git checkout --theirs path/to/file
```

> If you use the commands above, you still need to stage afterward.

### 4) Mark resolved (stage)

```bash
git add path/to/file
```

### 5) Finish the operation

### If it was a merge:

```bash
git commit
# or (if supported / preferred)
git merge --continue
```

### If it was a rebase:

```bash
git rebase --continue
```

## Abort / Back Out Safely

### Abort a merge

```bash
git merge --abort
```

### Abort a rebase

```bash
git rebase --abort
```

## Common Conflict Types

| Conflict Type    | Example                               | Typical Fix                                                 |
| ---------------- | ------------------------------------- | ----------------------------------------------------------- |
| Content conflict | same lines edited differently         | edit file, combine intent                                   |
| Modify/Delete    | one side deleted, other edited        | decide delete vs keep; `git rm` or keep file then `git add` |
| Add/Add          | both added same file path differently | choose one version or combine into one                      |

## Best Practices (Prevent + Reduce)

- Keep branches short-lived (integrate often)
- Rebase/merge main frequently before the branch diverges too much
- Avoid sweeping formatting changes mixed with logic changes
- Use small, atomic commits for easier rebase conflict resolution

## Related Notes

- [[git-merge]]
- [[git-rebase]]
- [[git-status]]
- [[git-diff]]
- [[git-add]]
- [[git-checkout]] (legacy conflict helpers)
- [[git-restore]] (file restore, not conflict-specific)
