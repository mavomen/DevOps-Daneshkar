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

## Related Notes

- [[CommitOperationsAndAdvanced]] — Extended coverage
