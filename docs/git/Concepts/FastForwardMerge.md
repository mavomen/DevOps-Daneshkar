---
id: FastForwardMerge
aliases: []
tags: []
---

# Fast Forward Merge

A fast-forward merge happens when Git can merge by simply moving the current branch pointer forward (no merge commit), because there is no divergence.

## When it happens

Fast-forward is possible when:

- the branch you are merging **into** is an ancestor of the branch you are merging **from**
- i.e., the target branch contains all commits of the current branch

## Visual

Before:

```txt
A---B   main
     \
      C---D   feature
```

After `git switch main && git merge feature`:

```txt
A---B---C---D   main, feature
```

No merge commit is created.

## Control flags

```bash
# allow only fast-forward, otherwise fail
git merge --ff-only feature

# force a merge commit even if ff is possible
git merge --no-ff feature
```

## Compare with three-way merge

If branches diverged, Git needs a merge commit:

- see [[ThreeWayMerge]]

## Related Notes

- [[git-merge]]
- [[ThreeWayMerge]]
- [[MergevsRebase]]
