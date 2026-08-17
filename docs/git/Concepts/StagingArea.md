---
id: StagingArea
aliases: []
tags: []
---

# Staging Area

The staging area (also called the index) is Git's preparation area where you collect changes before committing them to the repository.

## What is the Staging Area?

The staging area is:

- A buffer between your [[WorkingDirectory]] and [[GitHistory]]
- Where you prepare your next [[Commit]]
- Git's way of letting you control exactly what gets committed
- Part of [[TheThreeStates]] in Git workflow

## Why Use a Staging Area?

### Selective Committing

- Choose which changes to include in a commit
- Leave some changes for later commits
- Create focused, atomic commits
- Review changes before committing

### Quality Control

- Review what you're about to commit
- Catch mistakes before they enter history
- Organize changes logically
- Write better [[CommitMessageBestPractices|Commit Messages]].

## How the Staging Area Works

```mermaid
graph LR
    A[Working Directory] -->|git add| B[Staging Area]
    B -->|git commit| C[Repository]
    B -->|git restore --staged| A
    C -->|git restore| A
```

### File Movement

1. Modify files in [[WorkingDirectory]]
2. [[git-add]] moves changes to staging area
3. [[git-commit]] moves staged changes to repository
4. [[git-restore]] can undo staging or working changes

## Staging Area Commands

### Adding to Staging Area

```bash
# Stage specific file
git add filename.txt

# Stage all changes in current directory
git add .

# Stage all tracked files
git add -u

# Stage interactively (choose hunks)
git add -p

# Stage by file pattern
git add '*.js'
```

### Viewing Staging Area

```bash
# See staged vs unstaged changes
git status

# See what's staged for commit
git diff --staged
git diff --cached  # Same as --staged

# List staged files
git diff --staged --name-only
```

### Removing from Staging Area

```bash
# Unstage specific file
git restore --staged filename.txt

# Unstage all files
git restore --staged .

# Remove file from staging and working directory
git rm filename.txt

# Remove file from staging only
git rm --cached filename.txt
```

## Understanding Staged vs Unstaged

### Same File, Multiple States

A file can have:

- **Staged changes**: Ready for next commit
- **Unstaged changes**: Additional modifications

```bash
# Edit file
echo "Line 1" > file.txt
git add file.txt              # Stage first change

# Edit same file again
echo "Line 2" >> file.txt     # Unstaged change

# Now file has both staged and unstaged changes
git status
git diff                      # Shows unstaged changes
git diff --staged            # Shows staged changes
```

### Partial Staging

Stage only part of a file's changes:

```bash
# Interactive staging
git add -p filename.txt

# Options during interactive staging:
# y - stage this hunk
# n - don't stage this hunk
# s - split hunk into smaller parts
# e - manually edit hunk
# q - quit interactive mode
```

## Staging Area Best Practices

### Atomic Commits

- Stage related changes together
- Keep unrelated changes in separate commits
- Each commit should represent one logical change

### Review Before Committing

```bash
# Review staged changes
git diff --staged

# Check what's being committed
git status

# Ensure only intended changes are staged
git diff --staged --name-only
```

### Staging Workflow

```bash
# 1. Check current state
git status

# 2. See all changes
git diff

# 3. Stage selectively
git add specific-file.js
git add -p another-file.js

# 4. Review staged changes
git diff --staged

# 5. Commit staged changes
git commit -m "Implement feature X"

# 6. Continue with remaining changes
git diff  # See what's left unstaged
```

## Related Notes

- [[StagingAreaAdvanced]] — Extended coverage
