---
id: FileTrackingAndOperations
aliases: []
tags: []
---

# File Tracking & Operations

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

## Related Notes

- [[FileLifecycle]] — Core concepts
- [[FileTrackingAndOperations]] — This note
