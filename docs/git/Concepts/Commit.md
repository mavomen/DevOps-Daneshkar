---
id: Commit
aliases: []
tags: []
---

# Commit

A commit is a snapshot of your project at a specific point in time, containing all the changes you've staged along with metadata about when and who made the changes.

## What is a Commit?

A commit represents:

- A specific state of your project
- All files as they existed at commit time
- Metadata: author, date, commit message
- Link to parent commit(s) creating history
- Unique identifier ([[SHAHash]])

## Commit Components

### Commit Object Contents

```
commit 1a2b3c4d5e...
Author: John Doe <john@example.com>
Date: Mon Jan 15 10:30:45 2024 -0700

Add user authentication system

tree 5f6g7h8i9j...
parent 9k8l7m6n5o...
```

### Essential Elements

- **Tree**: Snapshot of all files
- **Parent**: Previous commit (creates history chain)
- **Author**: Who made the changes
- **Committer**: Who created the commit (usually same as author)
- **Timestamp**: When commit was created
- **Message**: Description of changes

## Creating Commits

### Basic Commit Process

```bash
# 1. Stage changes
git add file1.txt file2.js

# 2. Create commit
git commit -m "Add new feature"

# Or combine staging and committing (tracked files only)
git commit -am "Update existing files"
```

### Commit Message Formats

```bash
# Simple message
git commit -m "Fix login bug"

# Multi-line message
git commit -m "Add user authentication

- Implement JWT token system
- Add password hashing
- Create login/logout endpoints
- Add authentication middleware"

# Open editor for detailed message
git commit
```

### Amending Commits

```bash
# Change last commit message
git commit --amend -m "Better commit message"

# Add files to last commit
git add forgotten-file.txt
git commit --amend --no-edit

# Change author of last commit
git commit --amend --author="New Name <new@email.com>"
```

## Commit History

### Linear History

```
A ← B ← C ← D (main)
```

Each commit points to its parent, creating a chain.

### Branched History

```
    E ← F (feature)
   /
A ← B ← C ← D (main)
```

Branches create parallel commit chains.

### Merged History

```
    E ← F
   /     \
A ← B ← C ← D ← G (main)
```

Merges bring branches back together.

## Commit Identification

### SHA Hash

Every commit has unique identifier:

```bash
# Full hash
commit 1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b

# Short hash (first 7 characters)
1a2b3c4

# Git automatically uses shortest unambiguous hash
git log --oneline
```

### Relative References

```bash
# Current commit
HEAD

# Previous commit
HEAD~1
HEAD^

# Two commits ago
HEAD~2
HEAD^^

# First parent of merge commit
HEAD^1

# Second parent of merge commit
HEAD^2
```

## Commit Best Practices

### Atomic Commits

- One logical change per commit
- All related files changed together
- Commit compiles and passes tests
- Easy to revert if needed

### Good Commit Messages

```bash
# Good: Clear, concise, action-oriented
git commit -m "Fix memory leak in user session handling"
git commit -m "Add email validation to registration form"
git commit -m "Update dependencies to resolve security vulnerabilities"

# Bad: Vague, unclear, not helpful
git commit -m "fix stuff"
git commit -m "changes"
git commit -m "WIP"
```

### Commit Message Structure

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

Examples:

```bash
feat(auth): add JWT token authentication
fix(ui): resolve button alignment issues
docs(api): update endpoint documentation
refactor(db): optimize user query performance
```

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

## Related Concepts

- [[StagingArea]] - Preparing commits
- [[GitHistory]] - Chain of commits
- [[Branch]] - Parallel commit sequences
- [[git-commit]] - Creating commits
- [[SHAHash]] - Commit identification

## Quick Reference

| Command               | Purpose                     |
| --------------------- | --------------------------- |
| `git commit -m "msg"` | Create commit with message  |
| `git commit --amend`  | Modify last commit          |
| `git log --oneline`   | View commit history         |
| `git show <hash>`     | View specific commit        |
| `git revert <hash>`   | Undo commit with new commit |
