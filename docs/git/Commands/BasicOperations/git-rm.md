---
id: git-rm
aliases: []
tags: []
---

# git rm

Remove files from both the working directory and the Git index (staging area), scheduling them for deletion in the next commit.

## Syntax

```bash
git rm [<options>] [--] <file>...
```

## Description

The `git rm` command removes files from the Git repository and the working directory. Unlike regular `rm`, it stages the removal for the next [[Commit]], making Git aware that the file should no longer be tracked.

## Basic Usage

### Remove Single File

```bash
# Remove file from working directory and index
git rm filename.txt

# File is deleted and removal is staged
git status
# Changes to be committed:
#   deleted: filename.txt
```

### Remove Multiple Files

```bash
# Remove multiple specific files
git rm file1.txt file2.js file3.css

# Remove files by pattern
git rm '*.log'
git rm 'temp/*'

# Remove all files in directory
git rm -r directory/
```

## Options and Modes

### Keep File in Working Directory

```bash
# Remove from Git but keep file locally
git rm --cached filename.txt

# Useful for:
# - Files that should no longer be tracked
# - Adding files to .gitignore after they were tracked
# - Keeping local configuration files

# Example: Stop tracking but keep local config
git rm --cached config/local.json
echo "config/local.json" >> .gitignore
git add .gitignore
git commit -m "Stop tracking local config file"
```

### Force Removal

```bash
# Force remove files (override safety checks)
git rm -f filename.txt
git rm --force filename.txt

# Used when:
# - File has changes in working directory
# - File has changes in staging area
# - Git would normally prevent removal
```

### Recursive Removal

```bash
# Remove directories and their contents
git rm -r directory/
git rm --recursive directory/

# Remove multiple directories
git rm -r dir1/ dir2/ dir3/

# Combine with patterns
git rm -r 'test/**/temp'
```

### Dry Run

```bash
# See what would be removed without actually removing
git rm -n filename.txt
git rm --dry-run '*.temp'

# Preview recursive removal
git rm -n -r old-features/
```

## Common Scenarios

### Stop Tracking File

```bash
# File was accidentally tracked, now want to ignore
git rm --cached secrets.env

# Add to .gitignore to prevent future tracking
echo "secrets.env" >> .gitignore
git add .gitignore
git commit -m "Stop tracking secrets file"

# File remains in working directory but is no longer tracked
```

### Clean Up Repository

```bash
# Remove obsolete files
git rm old-script.sh deprecated-module.js

# Remove entire obsolete directories
git rm -r old-features/ legacy-code/

# Remove files matching pattern
git rm '*.backup' 'temp-*'

# Commit cleanup
git commit -m "Remove obsolete files and directories"
```

### Rename Workflow

```bash
# Git doesn't have explicit rename command
# Rename is implemented as remove + add

# Method 1: Use git mv (recommended)
git mv oldname.txt newname.txt

# Method 2: Manual rename using git rm
git rm oldname.txt
cp oldname.txt newname.txt  # Copy before removing
git add newname.txt
git commit -m "Rename oldname.txt to newname.txt"
```

## File States and git rm

### Modified Files

```bash
# File has uncommitted changes
echo "changes" >> important.txt
git rm important.txt
# error: the following file has local modifications:
#     important.txt

# Solutions:
# 1. Force removal (loses changes)
git rm -f important.txt

# 2. Commit changes first
git add important.txt
git commit -m "Save changes"
git rm important.txt

# 3. Stash changes
git stash
git rm important.txt
git commit -m "Remove file"
git stash pop  # If you want changes in a new file
```

### Staged Files

```bash
# File has staged changes
git add modified-file.txt
git rm modified-file.txt
# error: the following file has changes staged in the index:
#     modified-file.txt

# Solutions:
# 1. Force removal
git rm -f modified-file.txt

# 2. Unstage first, then remove
git restore --staged modified-file.txt
git rm modified-file.txt
```

### Untracked Files

```bash
# git rm only works with tracked files
touch new-untracked-file.txt
git rm new-untracked-file.txt
# fatal: pathspec 'new-untracked-file.txt' did not match any files

# Use regular rm for untracked files
rm new-untracked-file.txt

# Or use git clean for untracked files
git clean -f  # Remove untracked files
git clean -fd # Remove untracked files and directories
```

## Advanced Usage

### Conditional Removal

```bash
# Remove files that exist in working directory
git rm --ignore-unmatch nonexistent.txt  # Doesn't error if file missing

# Remove from index only if file doesn't exist in working directory
git rm --cached --ignore-unmatch removed-file.txt

# Useful in scripts where files may or may not exist
```

### Pattern Matching

```bash
# Remove all backup files
git rm '*.bak' '*.backup' '*~'

# Remove all files in temp directories
git rm 'temp/**/*'
git rm '**/temp/*'

# Remove log files recursively
git rm -r --cached 'logs/*.log'

# Complex patterns with pathspecs
git rm ':(glob)**/*.tmp'
git rm ':(icase)*.LOG'  # Case insensitive
```

### Integration with .gitignore

```bash
# Remove files that are now ignored
# First, add patterns to .gitignore
echo "*.log" >> .gitignore
echo "build/" >> .gitignore
echo ".env" >> .gitignore

# Remove currently tracked files that match ignore patterns
git rm --cached '*.log'
git rm -r --cached build/
git rm --cached .env

# Commit the .gitignore and removals
git add .gitignore
git commit -m "Add .gitignore and remove ignored files"
```

## Bulk Operations

### Remove All Files of Type

```bash
# Remove all log files
find . -name "*.log" -exec git rm {} \;

# Or using git with patterns
git rm '*.log'

# Remove all files in multiple extensions
git rm '*.tmp' '*.cache' '*.backup'
```

### Remove Based on git status

```bash
# Remove all deleted files (that were manually deleted)
git rm $(git ls-files --deleted)

# Or more safely with xargs
git ls-files --deleted -z | xargs -0 git rm

# Remove all files in staging that match pattern
git diff --name-only --cached | grep '\.tmp$' | xargs git rm --cached
```

### Scripted Removal

```bash
#!/bin/bash
# Remove old log files from Git tracking

# Find and remove log files older than 30 days
find . -name "*.log" -mtime +30 -exec git rm --cached {} \;

# Update .gitignore if not already present
if ! grep -q "*.log" .gitignore; then
    echo "*.log" >> .gitignore
    git add .gitignore
fi

# Commit changes
if ! git diff --cached --quiet; then
    git commit -m "Remove old log files from tracking and update .gitignore"
fi
```

## Recovery and Undo

### Undo git rm (Before Commit)

```bash
# Accidentally removed file
git rm important-file.txt

# Undo the removal (file comes back)
git restore --staged important-file.txt
git restore important-file.txt

# Or in one command
git reset HEAD important-file.txt
git checkout -- important-file.txt
```

### Undo git rm --cached

```bash
# Accidentally removed file from tracking
git rm --cached important-file.txt

# Add it back to tracking
git add important-file.txt

# Verify it's tracked again
git status
```

### Recover After Commit

```bash
# File was removed in previous commit
git log --oneline -5  # Find the commit

# Restore file from before it was removed
git restore --source=HEAD~1 deleted-file.txt

# Or checkout from specific commit
git checkout HEAD~1 -- deleted-file.txt

# Add back to repository
git add deleted-file.txt
git commit -m "Restore accidentally deleted file"
```

## Integration with Other Commands

### Working with git mv

```bash
# Move/rename is combination of rm and add
git mv oldname.txt newname.txt

# Equivalent to:
git rm oldname.txt
git add newname.txt
```

### Working with git clean

```bash
# git rm removes tracked files
# git clean removes untracked files

# Remove tracked files matching pattern
git rm '*.temp'

# Remove untracked files matching pattern
git clean -f -d  # Remove untracked files and directories

# Remove both tracked and untracked
git rm '*.temp' && git clean -f -d
```

### Working with git stash

```bash
# Stash before bulk removal
git stash push -m "Backup before cleanup"

# Remove files
git rm obsolete/ -r
git commit -m "Remove obsolete code"

# Restore stash if needed
git stash list
git stash pop  # If you need any of the removed files
```

## Performance Considerations

### Large Repositories

```bash
# For large numbers of files, use xargs
git ls-files '*.backup' | xargs git rm

# Or use find with git rm
find . -name "*.temp" -exec git rm {} +

# Batch operations in chunks
git ls-files '*.log' | head -100 | xargs git rm
```

### Network Repositories

```bash
# When working with large files over network
# Remove from index first, then from working directory
git rm --cached large-files/*
git commit -m "Remove large files from tracking"

# Clean up working directory separately
rm -rf large-files/
```

## Troubleshooting

### Permission Issues

```bash
# Permission denied when removing
sudo git rm protected-file.txt  # Not recommended

# Better: Fix permissions first
chmod +w protected-file.txt
git rm protected-file.txt
```

### Submodule Issues

```bash
# Removing submodules requires special handling
git rm submodule-directory
# May not work properly

# Proper submodule removal:
git submodule deinit submodule-directory
git rm submodule-directory
git commit -m "Remove submodule"
```

### Case Sensitivity

```bash
# On case-insensitive systems (Windows/macOS)
git rm File.txt
git add file.txt  # Different case

# May cause issues - be explicit about case
git rm --cached File.txt
git add file.txt
git commit -m "Fix filename case"
```

## Best Practices

### Before Removing

1. Review what will be removed: `git rm --dry-run`
2. Check file status: `git status`
3. Consider if file should be kept locally: use `--cached`
4. Update `.gitignore` if needed

### Safe Removal Workflow

```bash
# 1. Preview removal
git rm --dry-run '*.temp'

# 2. Check current status
git status

# 3. Backup important files if needed
cp important.temp important.temp.backup

# 4. Remove files
git rm '*.temp'

# 5. Update .gitignore if needed
echo "*.temp" >> .gitignore

# 6. Commit changes
git add .gitignore
git commit -m "Remove temp files and update gitignore"
```

### Team Coordination

- Communicate large file removals to team
- Update documentation when removing important files
- Consider deprecation period before removal
- Use meaningful commit messages for removals

## Related Commands

- [[git-add]] - Stage files for addition
- [[git-mv]] - Move/rename files
- [[git-status]] - Check file states
- [[git-clean]] - Remove untracked files
- [[FileLifecycle]] - Understanding file states

## Examples

```bash
# Basic file removal
git rm old-file.txt                   # Remove file completely
git rm --cached config.json           # Stop tracking but keep file

# Pattern-based removal
git rm '*.log'                        # Remove all log files
git rm -r temp/                       # Remove directory recursively

# Bulk operations
git rm $(git ls-files --deleted)      # Remove all manually deleted files
git rm --cached logs/*.log             # Stop tracking log files

# Force removal (when file has changes)
git rm -f modified-file.txt           # Force remove modified file

# Dry run and preview
git rm --dry-run '*.backup'           # Preview what would be removed
```
