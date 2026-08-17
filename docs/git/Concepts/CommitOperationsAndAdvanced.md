---
id: CommitOperationsAndAdvanced
aliases: []
tags: []
---

# Commit Operations & Advanced

## Viewing Commits

### Basic Log Views

```bash
# Standard log
git log

# Concise log
git log --oneline

# Graphical log
git log --graph --oneline --all

# Recent commits
git log -10

# Commits by author
git log --author="John Doe"
```

### Detailed Commit Information

```bash
# Show specific commit
git show 1a2b3c4

# Show commit with file changes
git show --stat 1a2b3c4

# Show commit with full diff
git show 1a2b3c4
```

### Searching Commits

```bash
# Search commit messages
git log --grep="bug fix"

# Search code changes
git log -S "function_name"

# Search by file
git log -- path/to/file.js

# Search by date range
git log --since="2024-01-01" --until="2024-01-31"
```

## Commit Operations

### Cherry-picking

```bash
# Apply specific commit to current branch
git cherry-pick 1a2b3c4

# Apply multiple commits
git cherry-pick 1a2b3c4 5d6e7f8
```

### Reverting

```bash
# Create new commit that undoes changes
git revert 1a2b3c4

# Revert without committing (for editing)
git revert --no-commit 1a2b3c4
```

### Resetting

```bash
# Move branch pointer (soft reset)
git reset --soft HEAD~1

# Unstage changes (mixed reset - default)
git reset HEAD~1

# Discard changes (hard reset - dangerous)
git reset --hard HEAD~1
```

## Advanced Commit Concepts

### Merge Commits

Special commits with multiple parents:

```bash
# Create merge commit
git merge feature-branch

# Merge commit has two parents
git show --format=fuller HEAD
```

### Empty Commits

```bash
# Create commit without changes (useful for triggers)
git commit --allow-empty -m "Trigger deployment"
```

### Signed Commits

```bash
# Sign commit with GPG key
git commit -S -m "Signed commit"

# Configure signing
git config user.signingkey YOUR_KEY_ID
git config commit.gpgsign true
```

## Commit Hooks

### Pre-commit Hooks

Run before commit is created:

- Code formatting
- Test execution
- Linting checks
- Security scans

### Post-commit Hooks

Run after commit is created:

- Notifications
- Deployment triggers
- Backup operations

## Common Commit Issues

### Accidental Commits

```bash
# Undo last commit, keep changes
git reset --soft HEAD~1

# Undo last commit, discard changes
git reset --hard HEAD~1

# Amend commit instead of new commit
git add forgotten-file.txt
git commit --amend --no-edit
```

### Large Commits

- Break into smaller, logical commits
- Use [[InteractiveRebase]] to split commits
- Stage changes selectively with [[git-add]]

### Bad Commit Messages

```bash
# Fix with amend (last commit only)
git commit --amend -m "Better message"

# Fix with rebase (older commits)
git rebase -i HEAD~3  # Edit commit messages
```

## Commit Performance

### Repository Size

- Commits store complete snapshots
- Git optimizes with compression and deltas
- Large files should use Git LFS
- Regular [[git-gc]] optimizes storage

### Commit Frequency

- Commit often for better history granularity
- Balance between too many and too few commits
- Use [[SquashingCommits]] to clean history before sharing

## Related Notes

- [[Commit]] — Core concepts
- [[CommitOperationsAndAdvanced]] — This note
