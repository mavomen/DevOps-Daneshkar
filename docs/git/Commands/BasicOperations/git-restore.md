---
id: git-restore
aliases: []
tags: []
---

# git restore

Restore files in the working directory or unstage files from the staging area. This is Git's modern command for discarding changes and managing file states.

## Syntax

```bash
git restore [<options>] [--source=<tree>] [--staged] [--worktree] [--] <pathspec>...
```

## Description

The `git restore` command was introduced in Git 2.23 as a cleaner alternative to some uses of `git checkout` and `git reset`. It's specifically designed for restoring files to different states and is safer because it only affects files, not branches or [[HEAD]].

## Basic Usage

### Restore Working Directory Files

```bash
# Discard changes in specific file
git restore filename.txt

# Discard changes in multiple files
git restore file1.txt file2.js file3.css

# Discard all changes in current directory
git restore .

# Discard all changes in repository
git restore :/
```

### Unstage Files

```bash
# Unstage specific file (remove from staging area)
git restore --staged filename.txt

# Unstage multiple files
git restore --staged file1.txt file2.js

# Unstage all staged files
git restore --staged .
```

### Combined Operations

```bash
# Unstage and discard changes (both staged and working directory)
git restore --staged --worktree filename.txt

# Shorthand for both (default behavior when both areas specified)
git restore --staged --worktree .
```

## Target Specification

### Working Tree Operations

```bash
# Restore working directory (default)
git restore filename.txt
git restore --worktree filename.txt  # Explicit

# Restore specific directory
git restore src/

# Restore by pattern
git restore '*.js'
git restore 'src/**/*.css'
```

### Staging Area Operations

```bash
# Unstage files
git restore --staged filename.txt

# Unstage directory
git restore --staged src/

# Unstage all changes
git restore --staged .
```

### Both Areas

```bash
# Restore in both staging and working directory
git restore --staged --worktree filename.txt

# Using shorthand --source=HEAD (same effect)
git restore --source=HEAD filename.txt
```

## Source Specification

### Restore from Different Commits

```bash
# Restore from specific commit
git restore --source=HEAD~1 filename.txt

# Restore from specific commit hash
git restore --source=1a2b3c4 filename.txt

# Restore from different branch
git restore --source=main filename.txt
git restore --source=feature-branch src/app.js
```

### Restore from Tags

```bash
# Restore file from tagged version
git restore --source=v1.0.0 config.json

# Restore multiple files from tag
git restore --source=v2.1.0 src/ docs/
```

### Restore from Index

```bash
# Restore working directory from staging area (default)
git restore filename.txt

# Explicit source specification
git restore --source=index filename.txt
```

## Advanced Options

### Path Specification

```bash
# Restore files matching pathspec
git restore 'src/**/*.js'

# Restore everything except specific files
git restore . ':(exclude)*.log'

# Restore files in specific subdirectories
git restore src/ tests/

# Use quotes for complex patterns
git restore ':(glob)**/*.{js,ts,jsx,tsx}'
```

### Interactive Restoration

```bash
# Restore selectively (patch mode)
git restore -p filename.txt
git restore --patch filename.txt

# Interactive patch mode options:
# y - discard this hunk
# n - do not discard this hunk
# q - quit; do not discard this hunk or any remaining ones
# a - discard this hunk and all later hunks in the file
# d - do not discard this hunk or any later hunks in the file
# s - split the current hunk into smaller hunks
# e - manually edit the current hunk
# ? - print help
```

### Overlay and Merge Modes

```bash
# Overlay mode (default) - only restore existing files
git restore filename.txt

# No-overlay mode - restore all files from source, removing others
git restore --no-overlay --source=HEAD~1 src/

# Useful for completely reverting directory to previous state
git restore --no-overlay --source=v1.0.0 config/
```

## Common Workflows

### Undoing Modifications

```bash
# Made mistake in file, want to revert
echo "wrong content" >> important-file.txt
git status  # Shows modified file

# Restore to last committed version
git restore important-file.txt
git status  # File no longer modified
```

### Unstaging Accidentally Added Files

```bash
# Accidentally staged wrong file
git add .
git status  # Shows many staged files

# Unstage specific files
git restore --staged unwanted-file.txt
git restore --staged temp/

# Or unstage everything and start over
git restore --staged .
git add intended-files
```

### Switching Between File Versions

```bash
# Try different version of configuration
git restore --source=experimental-branch config.json

# Test with it...

# Switch to production version
git restore --source=production-branch config.json

# Or back to current branch version
git restore config.json
```

### Partial File Restoration

```bash
# File has good and bad changes
git add -p important-file.js  # Stage good changes

# Restore working directory to remove bad changes
git restore important-file.js

# Now only good changes are staged for commit
git commit -m "Implement feature (good changes only)"
```

## File State Examples

### New File Scenarios

```bash
# Created new file and staged it
echo "new content" > newfile.txt
git add newfile.txt

# Unstage new file
git restore --staged newfile.txt
# File still exists but is untracked

# Remove new file completely
rm newfile.txt  # Git restore doesn't remove untracked files
```

### Modified File Scenarios

```bash
# Modified existing file
echo "changes" >> existing.txt
git add existing.txt         # Stage changes
echo "more changes" >> existing.txt  # More changes

# Current state:
# - Staged: original + "changes"
# - Working: original + "changes" + "more changes"

# Restore working directory to staged version
git restore existing.txt
# Working directory now matches staged version

# Unstage to get back to original
git restore --staged existing.txt
```

### Deleted File Scenarios

```bash
# Accidentally deleted tracked file
rm important.txt
git status  # Shows file as deleted

# Restore deleted file
git restore important.txt
# File is back with original content

# If deletion was staged
git rm important.txt  # Stages deletion
git restore --staged important.txt  # Unstages deletion
git restore important.txt  # Restores file content
```

## Integration with Git Workflow

### Pre-Commit Cleanup

```bash
# Before committing, clean up unwanted changes
git status                    # See current state
git restore debug-file.js     # Remove debug changes
git restore --staged temp.log # Unstage temporary files
git status                    # Verify clean state
git commit -m "Clean feature implementation"
```

### Experimental Development

```bash
# Save current state
git add .
git commit -m "Checkpoint before experiment"

# Make experimental changes
# ... edit files ...

# If experiment fails, restore to checkpoint
git restore .

# If experiment succeeds, keep changes
git add .
git commit -m "Successful experiment"
```

### Collaborative Development

```bash
# Pull latest changes but have local modifications
git status                 # See local changes
git stash                 # Save local changes
git pull origin main      # Update from remote
git stash pop            # Restore local changes

# If conflicts, use restore to resolve
git restore --staged conflicted-file.txt  # Unstage
git restore conflicted-file.txt           # Use remote version
# Or manually resolve and commit
```

## Safety and Recovery

### Before Restoring

```bash
# Always check what will be lost
git status
git diff filename.txt

# For large changes, consider stashing first
git stash push -m "backup before restore"
git restore filename.txt
# If needed: git stash pop
```

### Recovering from Accidental Restore

```bash
# If you accidentally restored a file
# Check reflog for recent commits
git reflog

# Or check if you have it staged elsewhere
git stash list

# Look for the content in previous commits
git log --oneline -p -- filename.txt

# Restore from specific commit if found
git restore --source=<commit-hash> filename.txt
```

## Comparison with Legacy Commands

### git restore vs git checkout

```bash
# Old way (git checkout - still works but confusing)
git checkout -- filename.txt        # Restore file
git checkout HEAD -- filename.txt   # Restore from specific commit

# New way (git restore - clearer intent)
git restore filename.txt             # Restore file
git restore --source=HEAD filename.txt  # Restore from specific commit
```

### git restore vs git reset

```bash
# Old way (git reset - still works)
git reset HEAD filename.txt          # Unstage file
git reset --hard HEAD filename.txt   # Dangerous: affects HEAD

# New way (git restore - safer)
git restore --staged filename.txt    # Unstage file
git restore filename.txt             # Restore file (no HEAD movement)
```

## Performance Considerations

### Large Files and Directories

```bash
# Restore specific files rather than entire directories
git restore src/specific-file.js     # Fast
git restore src/                     # May be slow for large directories

# Use patterns to limit scope
git restore 'src/**/*.js'            # Only JavaScript files
```

### Remote Sources

```bash
# Restoring from remote sources may be slower
git restore --source=origin/main filename.txt

# Consider fetching first for better performance
git fetch origin
git restore --source=origin/main filename.txt
```

## Troubleshooting

### Common Errors

```bash
# File not found in source
git restore --source=wrong-branch nonexistent.txt
# error: pathspec 'nonexistent.txt' did not match any files

# Invalid source
git restore --source=nonexistent-commit filename.txt
# fatal: invalid reference: nonexistent-commit

# Nothing to restore
git restore clean-file.txt  # File hasn't changed
# (No error, no operation)
```

### Path Issues

```bash
# Use quotes for special characters
git restore "file with spaces.txt"

# Escape special characters if needed
git restore file\#with\#hash.txt

# Use -- to separate options from paths
git restore --staged -- -weird-filename.txt
```

## Examples

```bash
# Basic file restoration
git restore modified-file.txt         # Discard working directory changes
git restore --staged added-file.txt   # Unstage file

# Restore from different sources
git restore --source=HEAD~1 config.js # Restore from previous commit
git restore --source=main app.js      # Restore from main branch

# Interactive and selective operations
git restore -p large-file.js          # Selectively discard changes
git restore --staged .                # Unstage all changes

# Directory operations
git restore src/                      # Restore entire directory
git restore '*.js'                   # Restore all JavaScript files

# Combined operations
git restore --staged --worktree file.txt  # Unstage and discard changes
```


## Related Notes

- [[git-status]] - Check what files need restoration
- [[git-diff]] - See what changes would be lost
- [[git-stash]] - Temporarily save changes
- [[git-checkout]] - Legacy command for some restore operations
- [[git-reset]] - Alternative for unstaging (with caveats)
