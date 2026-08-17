---
id: HEADInternalsAndPractical
aliases: []
tags: []
---

# HEAD Internals & Practical

## HEAD Movement Examples

### Basic Navigation

```bash
# Start on main branch
git switch main
# HEAD -> main -> latest-commit

# Go back one commit (detached)
git checkout HEAD~1
# HEAD -> previous-commit

# Return to main
git switch main
# HEAD -> main -> latest-commit
```

### During Merge

```bash
# Before merge
HEAD -> main -> commit-C

# During merge (if conflicts)
# HEAD still points to main
# Working directory has merge state

# After successful merge
HEAD -> main -> new-merge-commit
```

### During Rebase

```bash
# Before rebase
HEAD -> feature -> commit-E

# During rebase
# HEAD moves through commits being replayed

# After rebase
HEAD -> feature -> rebased-commit-E'
```

## HEAD in Git Internals

### Physical Storage

```bash
# HEAD file location
cat .git/HEAD

# Points to current branch file
cat .git/refs/heads/main

# Which contains commit hash
1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b
```

### HEAD Movement Tracking

```bash
# See HEAD movement history
git reflog

# Shows entries like:
# 1a2b3c4 HEAD@{0}: checkout: moving from main to feature
# 5d6e7f8 HEAD@{1}: commit: Add new feature
# 9g8h7i6 HEAD@{2}: checkout: moving from feature to main
```

## Practical HEAD Usage

### Quick Navigation

```bash
# Jump to previous commit quickly
git show HEAD~1

# Compare recent commits
git diff HEAD~2..HEAD

# Create branch from earlier state
git branch backup HEAD~5
```

### Undoing Changes

```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Undo multiple commits
git reset --hard HEAD~3
```

### Finding Information

```bash
# What commit is HEAD?
git rev-parse HEAD

# What branch is HEAD on?
git branch --show-current

# Where has HEAD been?
git reflog --oneline
```

## HEAD Best Practices

### Safe Navigation

- Understand detached HEAD before using
- Create branches for experimental work
- Use `git switch` instead of `git checkout` for branches
- Check `git status` regularly

### Recovery Planning

- Know how to use `git reflog`
- Understand how to create recovery branches
- Regular commits make recovery easier
- Keep important work on named branches

### Team Collaboration

- Don't push detached HEAD commits
- Communicate when doing complex HEAD operations
- Use descriptive branch names
- Document unusual HEAD manipulations

## Troubleshooting HEAD Issues

### Lost Commits in Detached HEAD

```bash
# Find lost commits
git reflog

# Create branch from lost commit
git branch recovery <commit-hash>

# Or reset current branch
git reset --hard <commit-hash>
```

### Confused About Current Position

```bash
# Check current HEAD position
git log --oneline -1
git status
git branch

# Visual representation
git log --graph --oneline --all
```

### HEAD File Corruption

```bash
# If HEAD file is corrupted
echo "ref: refs/heads/main" > .git/HEAD

# Verify fix
git status
```

## Related Notes

- [[HEAD]] — Core concepts
- [[HEADInternalsAndPractical]] — This note
