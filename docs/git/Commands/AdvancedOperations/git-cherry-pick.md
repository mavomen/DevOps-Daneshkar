---
id: git-cherry-pick
aliases: []
tags: []
---

# git cherry-pick

Apply one (or more) existing commits onto your current branch.

## Syntax

```bash
git cherry-pick <commit>...
git cherry-pick <commit-range>
git cherry-pick --continue | --abort | --skip
```

## Description

`git cherry-pick` takes the changes introduced by an existing commit and re-applies them as a new commit on your current branch.

It’s useful for:

- bringing a hotfix commit from `main` into `develop`
- selecting a small subset of commits from a feature branch
- backporting fixes to a release branch

Cherry-picking **copies changes**, not “moving” the original commit, so the new commit will have a different [[SHAHash]].

## Basic Usage

### Cherry-pick a single commit

```bash
git cherry-pick <commit-hash>
```

### Cherry-pick multiple commits

```bash
git cherry-pick <hash1> <hash2> <hash3>
```

### Cherry-pick a range of commits

```bash
# commits after OLDEST up to and including NEWEST
git cherry-pick OLDEST^..NEWEST
```

## Options

### Edit commit message

```bash
git cherry-pick -e <commit>
```

### Don’t commit immediately (stage changes, then commit yourself)

```bash
git cherry-pick --no-commit <commit>
git status
git commit -m "Custom message"
```

### Resolve conflicts workflow

```bash
# after you resolve conflicts and stage files:
git add .
git cherry-pick --continue
```

Abort:

```bash
git cherry-pick --abort
```

Skip the problematic commit:

```bash
git cherry-pick --skip
```

## Troubleshooting

### Conflicts

Conflict resolution is the standard pattern:

- resolve files
- `git add ...`
- `git cherry-pick --continue`

See: [[ConflictResolution]]

### “Empty” cherry-pick

Sometimes the commit changes already exist (e.g., applied via another commit). Git may report an empty cherry-pick; you can:

- skip: `git cherry-pick --skip`
- or allow empty commit if you intentionally want it (rare)

## Related Commands

- [[git-rebase]] - reapply a whole series of commits (often better for “move branch base”)
- [[git-merge]] - integrate full branch history
- [[git-revert]] - undo a commit safely on shared branches
- [[git-log]] / [[git-show]] - find and inspect commits

## Examples

```bash
# Backport a fix to a release branch
git switch release/v1.2
git cherry-pick <fix-commit>

# Move a single commit from feature branch to main
git switch main
git cherry-pick <commit-from-feature>
```
