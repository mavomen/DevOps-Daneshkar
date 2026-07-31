---
id: git-status
aliases: []
tags: []
---

# git status

Display the current state of the working directory and staging area, showing which files are tracked, modified, staged, or untracked.

## Syntax

```bash
git status [<options>]
```

## Description

The `git status` command shows the current state of your [[WorkingDirectory]] and [[StagingArea]]. It displays which files have been modified, which changes are staged for commit, which files aren't being tracked by Git, and other useful information about your repository state.

## Basic Usage

### Standard Status Output

```bash
# Show full status
git status

# Example output:
# On branch main
# Your branch is up to date with 'origin/main'.
#
# Changes to be committed:
#   (use "git restore --staged <file>..." to unstage)
#         modified:   src/app.js
#         new file:   src/auth.js
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git restore <file>..." to discard changes in working directory)
#         modified:   README.md
#         deleted:    old-file.txt
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         config.json
#         temp.log
```

### Short Status Format

```bash
# Concise status output
git status -s
git status --short

# Example output:
# M  src/app.js     # Modified and staged
# A  src/auth.js    # Added (new file staged)
#  M README.md      # Modified but not staged
#  D old-file.txt   # Deleted but not staged
# ?? config.json    # Untracked file
# ?? temp.log       # Untracked file
```

### Porcelain Format

```bash
# Machine-readable format
git status --porcelain
git status --porcelain=v1  # Version 1 format
git status --porcelain=v2  # Version 2 format (more detailed)
```

## Status Symbols

### Short Format Symbols

| Symbol | Meaning                 |
| ------ | ----------------------- |
| `??`   | Untracked file          |
| `A`    | Added (new file staged) |
| `M`    | Modified                |
| `D`    | Deleted                 |
| `R`    | Renamed                 |
| `C`    | Copied                  |
| `U`    | Updated but unmerged    |

### Two-Character Format

```
XY filename
```

- **X**: Status of file in staging area
- **Y**: Status of file in working directory

| XY   | Meaning                                              |
| ---- | ---------------------------------------------------- |
| ` M` | Modified in working directory                        |
| `M ` | Modified in staging area                             |
| `MM` | Modified in both staging and working directory       |
| `A ` | Added to staging area                                |
| `AM` | Added to staging, then modified in working directory |
| `D ` | Deleted in staging area                              |
| ` D` | Deleted in working directory                         |
| `??` | Untracked                                            |

## Advanced Options

### Branch Information

```bash
# Show branch and tracking info
git status -b
git status --branch

# Example output:
# On branch feature/new-auth
# Your branch is ahead of 'origin/feature/new-auth' by 2 commits.
#   (use "git push" to publish your local commits)
```

### Ignored Files

```bash
# Show ignored files
git status --ignored

# Show ignored files with short format
git status --ignored -s
```

### Untracked Files Control

```bash
# Hide untracked files
git status -u no
git status --untracked-files=no

# Show all untracked files (default)
git status -u normal
git status --untracked-files=normal

# Show all files in untracked directories
git status -u all
git status --untracked-files=all
```

### Ahead/Behind Information

```bash
# Show ahead/behind counts
git status --ahead-behind

# Disable ahead/behind calculation (faster for large repos)
git status --no-ahead-behind
```

## Understanding Status Output

### Clean Working Directory

```bash
git status

# Output when nothing to commit:
# On branch main
# Your branch is up to date with 'origin/main'.
#
# nothing to commit, working tree clean
```

### Files in Different States

```bash
# Create example scenario
echo "new content" > new-file.txt          # Untracked
echo "modified" >> existing-file.txt       # Modified
git add new-file.txt                       # Staged new file
git add existing-file.txt                  # Staged modification
echo "more changes" >> existing-file.txt   # Modified again after staging

git status
# On branch main
# Changes to be committed:
#         new file:   new-file.txt
#         modified:   existing-file.txt
#
# Changes not staged for commit:
#         modified:   existing-file.txt
```

### Branch Tracking Status

```bash
git status

# Possible branch status messages:
# "Your branch is up to date with 'origin/main'"
# "Your branch is ahead of 'origin/main' by 2 commits"
# "Your branch is behind 'origin/main' by 1 commit"
# "Your branch and 'origin/main' have diverged"
```

## Common Status Patterns

### Development Workflow

```bash
# 1. Check current state
git status
# On branch feature/user-auth
# nothing to commit, working tree clean

# 2. Make changes
echo "auth logic" > auth.js
echo "updated" >> app.js

# 3. Check what changed
git status
# Untracked files: auth.js
# Changes not staged: app.js

# 4. Stage changes selectively
git add auth.js

# 5. Check staging state
git status
# Changes to be committed: new file: auth.js
# Changes not staged: modified: app.js

# 6. Stage remaining changes
git add app.js

# 7. Final status check before commit
git status
# Changes to be committed:
#   new file: auth.js
#   modified: app.js
```

### Merge Conflict Status

```bash
git status

# During merge conflict:
# On branch main
# You have unmerged paths.
#   (fix conflicts and run "git commit")
#   (use "git merge --abort" to abort the merge)
#
# Unmerged paths:
#   (use "git add <file>..." to mark resolution)
#         both modified:   conflicted-file.txt
```

### Rebase Status

```bash
git status

# During rebase:
# interactive rebase in progress; onto 1a2b3c4
# Last command done (1 command done):
#    pick 5d6e7f8 Add feature
# Next commands to do (2 remaining commands):
#    pick 9g8h7i6 Fix bug
#    pick 2j3k4l5 Update docs
#   (use "git rebase --edit-todo" to view and edit)
# You are currently editing a commit while rebasing branch 'feature' on '1a2b3c4'.
#   (use "git commit --amend" to amend the current commit)
#   (use "git rebase --continue" once you are satisfied with your changes)
```

## Status with Other Commands

### Status in Scripts

```bash
#!/bin/bash

# Check if working directory is clean
if git diff-index --quiet HEAD --; then
    echo "Working directory is clean"
else
    echo "Working directory has uncommitted changes"
    git status --short
    exit 1
fi

# Check if ahead of remote
LOCAL=$(git rev-parse @)
REMOTE=$(git rev-parse @{u})

if [ $LOCAL = $REMOTE ]; then
    echo "Up-to-date with remote"
elif [ $LOCAL = $(git merge-base @ @{u}) ]; then
    echo "Need to pull from remote"
elif [ $REMOTE = $(git merge-base @ @{u}) ]; then
    echo "Need to push to remote"
else
    echo "Diverged from remote"
fi
```

### Status with Watch

```bash
# Monitor status changes in real-time
watch -n 2 git status --short

# Or with color
watch -n 2 --color git -c color.status=always status --short
```

## Customizing Status Output

### Configuration Options

```bash
# Always show short status
git config --global status.short true

# Always show branch info
git config --global status.branch true

# Control untracked files display
git config --global status.showUntrackedFiles normal

# Show stash count in status
git config --global status.showStash true

# Use relative paths in status
git config --global status.relativePaths true
```

### Color Configuration

```bash
# Enable colored output
git config --global color.status auto

# Customize status colors
git config --global color.status.added "green bold"
git config --global color.status.changed "yellow"
git config --global color.status.untracked "red"
git config --global color.status.header "white"
git config --global color.status.branch "cyan bold"
```

### Custom Status Aliases

```bash
# Create useful status aliases
git config --global alias.st "status --short --branch"
git config --global alias.stat "status"
git config --global alias.s "status --short"

# Use aliases
git st    # Short status with branch info
git s     # Very short status
git stat  # Full status
```

## Performance Considerations

### Large Repositories

```bash
# Disable ahead/behind calculation for performance
git status --no-ahead-behind

# Or set permanently
git config --global status.aheadBehind false

# Disable untracked files scanning
git status --untracked-files=no
```

### Status in Subdirectories

```bash
# Status shows files relative to current directory
cd src/
git status
# Shows only files in src/ and subdirectories

# To see full repository status from anywhere
git status --porcelain | head -20
```

## Troubleshooting Status Issues

### Status Shows No Changes But Files Modified

```bash
# Check line ending issues
git config core.autocrlf

# Check file permissions (if core.filemode is true)
git config core.filemode

# Check if files are ignored
git check-ignore filename.txt

# Force refresh index
git update-index --refresh
```

### Status Very Slow

```bash
# Check repository size
git count-objects -v

# Enable file system monitor (if available)
git config core.fsmonitor true

# Use git maintenance
git maintenance start

# Check for large untracked directories
git clean -fd  # Remove untracked files and directories
```

### Confused Status After Merge/Rebase

```bash
# Check if in middle of operation
ls .git/MERGE_HEAD  # Merge in progress
ls .git/rebase-apply/  # Rebase in progress

# Clean up if needed
git merge --abort    # Abort merge
git rebase --abort   # Abort rebase
```

## Related Commands

- [[git-diff]] - See actual changes in files
- [[git-add]] - Stage changes shown in status
- [[git-restore]] - Undo changes shown in status
- [[FileLifecycle]] - Understanding file states
- [[TheThreeStates]] - Git's file state model

## Examples

```bash
# Basic status checking workflow
git status                    # Full status
git status -s                 # Short status
git status -sb                # Short with branch info

# Development workflow
git status                    # Check current state
# ... make changes ...
git status                    # See what changed
git add .                     # Stage changes
git status                    # Verify staging
git commit -m "Update code"   # Commit changes
git status                    # Confirm clean state

# Checking specific aspects
git status --ignored          # Include ignored files
git status --untracked-files=all  # Show all untracked
git status --porcelain        # Machine readable format
```
