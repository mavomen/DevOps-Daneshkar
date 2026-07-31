---
id: FileLifecycle
aliases: []
tags: []
---

# File Lifecycle

The file lifecycle in Git describes how files transition through different states as they're tracked, modified, staged, and committed within the Git workflow.

## File States Overview

Files in a Git repository can exist in four primary states:

```mermaid
graph LR
    A[Untracked] --> B[Staged]
    B --> C[Committed]
    C --> D[Modified]
    D --> B
    D --> E[Unstaged]
    E --> B
    C --> F[Deleted]
    F --> B
```

### The Four States

1. **Untracked**: Git doesn't know about the file
2. **Staged**: File changes are prepared for commit
3. **Committed**: File is stored in Git database
4. **Modified**: File has been changed since last commit

## Detailed File States

### Untracked Files

- New files not yet added to Git
- Files matching [[GitIgnorePatterns]]
- Temporary files and build artifacts

```bash
# See untracked files
git status
# Shows: Untracked files: (use "git add <file>..." to include)

# Add untracked file to staging
git add newfile.txt
```

### Staged Files

- Files added to the [[StagingArea]]
- Changes prepared for next commit
- Can be unstaged before committing

```bash
# Stage specific file
git add modified-file.js

# Stage all changes
git add .

# See staged files
git status
# Shows: Changes to be committed:

# Unstage file
git restore --staged modified-file.js
```

### Committed Files

- Files stored in Git's database
- Part of repository history
- Associated with specific [[Commit]]

```bash
# Commit staged files
git commit -m "Add new feature"

# Files are now committed and tracked
git status
# Shows: nothing to commit, working tree clean
```

### Modified Files

- Tracked files with unsaved changes
- Different from last committed version
- Need staging before next commit

```bash
# Modify existing file
echo "new content" >> existing-file.txt

# See modified files
git status
# Shows: Changes not staged for commit:

# See what changed
git diff
```

## File Transitions

### New File Journey

```bash
# 1. Create new file (Untracked)
echo "Hello World" > hello.txt
git status  # Shows as untracked

# 2. Add to staging (Staged)
git add hello.txt
git status  # Shows as staged

# 3. Commit file (Committed)
git commit -m "Add hello.txt"
git status  # Working tree clean

# 4. Modify file (Modified)
echo "Updated" >> hello.txt
git status  # Shows as modified

# 5. Stage changes (Staged)
git add hello.txt
git status  # Shows as staged for commit

# 6. Commit changes (Committed)
git commit -m "Update hello.txt"
```

### File State Commands

```bash
# Check overall status
git status

# Short status format
git status -s
# ?? = untracked
# A  = added (staged)
# M  = modified
#  M = modified but not staged
# MM = modified, staged, then modified again

# See differences
git diff            # Working directory vs staged
git diff --staged   # Staged vs last commit
git diff HEAD       # Working directory vs last commit
```

## Complex File States

### Partially Staged Files

A file can have both staged and unstaged changes:

```bash
# Modify file
echo "Line 1" > file.txt
git add file.txt        # Stage first change

# Modify again
echo "Line 2" >> file.txt

# Now file has both staged and unstaged changes
git status
# Changes to be committed:
#   modified: file.txt
# Changes not staged for commit:
#   modified: file.txt
```

### Renamed Files

Git tracks file renames:

```bash
# Rename file
git mv oldname.txt newname.txt
git status
# Shows: renamed: oldname.txt -> newname.txt

# Manual rename (Git detects similarity)
mv file1.txt file2.txt
git rm file1.txt
git add file2.txt
git status
# May show: renamed: file1.txt -> file2.txt
```

### Deleted Files

```bash
# Delete file from working directory
rm unwanted.txt
git status
# Shows: deleted: unwanted.txt

# Stage the deletion
git add unwanted.txt
# or
git rm unwanted.txt

# Commit deletion
git commit -m "Remove unwanted file"
```

## File State Management

### Staging Strategies

```bash
# Stage all tracked files
git add -u

# Stage all files (including new ones)
git add .

# Interactive staging
git add -p
# Lets you stage parts of files

# Stage by pattern
git add '*.js'
```

### Unstaging Changes

```bash
# Unstage specific file
git restore --staged filename.txt

# Unstage all files
git restore --staged .

# Legacy syntax
git reset HEAD filename.txt
```

### Discarding Changes

```bash
# Discard working directory changes
git restore filename.txt

# Discard all working directory changes
git restore .

# Remove untracked files
git clean -f

# Remove untracked files and directories
git clean -fd
```

## File Tracking Patterns

### Selective Tracking

```bash
# Track specific file types
git add '*.js' '*.css'

# Track directory
git add src/

# Track everything except specific files
git add .
git reset HEAD unwanted-file.txt
```

### Ignore Patterns

```bash
# Create .gitignore
echo "*.log" >> .gitignore
echo "node_modules/" >> .gitignore
git add .gitignore
git commit -m "Add gitignore file"

# Now .log files and node_modules/ are ignored
```

## File History Tracking

### Following File Changes

```bash
# See file history
git log -- filename.txt

# Follow through renames
git log --follow -- filename.txt

# See what changed in each commit
git log -p -- filename.txt

# See when file was created
git log --diff-filter=A -- filename.txt
```

### File Blame

```bash
# See who changed each line
git blame filename.txt

# Blame specific lines
git blame -L 10,20 filename.txt

# Follow through renames
git blame -C filename.txt
```

## Working Directory Management

### Clean Working Directory

```bash
# Check if working directory is clean
git status

# Commit all changes
git add .
git commit -m "Save current work"

# Or stash changes
git stash
```

### File Recovery

```bash
# Restore deleted file from last commit
git restore filename.txt

# Restore file from specific commit
git restore --source=HEAD~2 filename.txt

# Restore file from specific commit to staging
git restore --source=HEAD~2 --staged filename.txt
```

## File State Best Practices

### Daily Workflow

1. Check status frequently: `git status`
2. Review changes before staging: `git diff`
3. Stage selectively: `git add <specific-files>`
4. Review staged changes: `git diff --staged`
5. Commit with meaningful message
6. Keep working directory clean

### File Organization

- Use meaningful file and directory names
- Group related files together
- Keep large files out of Git (use Git LFS)
- Use `.gitignore` for generated files

### Commit Strategies

- Stage related changes together
- Make atomic commits
- Don't commit debugging code
- Test before committing
- Write clear commit messages

## Common File State Issues

### Accidentally Staged Wrong Files

```bash
# Unstage specific file
git restore --staged wrong-file.txt

# Unstage all and restage correctly
git restore --staged .
git add correct-file.txt
```

### Modified File Won't Stage

```bash
# Check if file is in .gitignore
git check-ignore filename.txt

# Force add ignored file
git add -f filename.txt

# Check file permissions
ls -la filename.txt
```

### Lost Changes

```bash
# Check reflog for recent changes
git reflog

# Find lost commits
git fsck --lost-found

# Restore from stash if available
git stash list
git stash apply stash@{0}
```

## File State Automation

### Pre-commit Hooks

```bash
# Example pre-commit hook
#!/bin/sh
# Run tests before commit
npm test || exit 1

# Format code
prettier --write .
git add .
```

### IDE Integration

Most editors show file states:

- Green: New files
- Blue: Modified files
- Red: Deleted files
- Gray: Ignored files

## Advanced File Operations

### Sparse Checkout

```bash
# Only checkout specific directories
git config core.sparseCheckout true
echo "src/*" >> .git/info/sparse-checkout
git read-tree -m -u HEAD
```

### Large File Handling

```bash
# Initialize Git LFS for large files
git lfs install
git lfs track "*.psd"
git add .gitattributes

# Add large file
git add large-file.psd
git commit -m "Add large design file"
```

## Related Concepts

- [[WorkingDirectory]] - Where file changes occur
- [[StagingArea]] - Preparation area for commits
- [[git-status]] - Checking file states
- [[git-add]] - Moving files to staging
- [[git-restore]] - Undoing file changes

## Quick Reference

| State                | Command to Enter | Command to Exit               |
| -------------------- | ---------------- | ----------------------------- |
| Untracked → Staged   | `git add <file>` | `git restore --staged <file>` |
| Modified → Staged    | `git add <file>` | `git restore --staged <file>` |
| Staged → Committed   | `git commit`     | N/A (history is permanent)    |
| Committed → Modified | Edit file        | `git restore <file>`          |
