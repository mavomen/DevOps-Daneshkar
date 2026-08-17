---
id: git-branch
aliases: []
tags: []
---

# git branch

Create, list, rename, and delete branches. The fundamental command for managing parallel lines of development.

## Syntax

```bash
git branch [<options>] [<branch-name>] [<start-point>]
```

## Description

The `git branch` command is the primary tool for [[Branch]] management in Git. It allows you to create new branches, list existing branches, rename branches, and delete branches. Branches enable parallel development and feature isolation.

## Basic Usage

### List Branches

```bash
# List local branches
git branch

# Example output:
#   feature/user-auth
# * main
#   release/v2.0

# List all branches (local + remote)
git branch -a
git branch --all

# List only remote branches
git branch -r
git branch --remotes
```

### Create New Branch

```bash
# Create new branch from current commit
git branch feature/new-feature

# Create branch from specific commit
git branch hotfix/bug-123 1a2b3c4

# Create branch from another branch
git branch feature/auth main
git branch feature/payment feature/auth

# Create branch from tag
git branch hotfix/v1.1.1 v1.1.0
```

### Delete Branches

```bash
# Delete merged branch (safe)
git branch -d feature/completed-feature

# Force delete unmerged branch
git branch -D experimental-feature

# Delete multiple branches
git branch -d feature/old-1 feature/old-2 hotfix/temp
```

## Branch Information

### Verbose Output

```bash
# Show last commit on each branch
git branch -v

# Example output:
#   feature/auth    1a2b3c4 Add JWT authentication
# * main            5d6e7f8 Update README
#   release/v2.0    9g8h7i6 Prepare release notes

# Show even more details
git branch -vv

# Example output (with tracking info):
#   feature/auth           1a2b3c4 [origin/feature/auth] Add JWT
# * main                   5d6e7f8 [origin/main: ahead 2] Update README
#   release/v2.0           9g8h7i6 Prepare release notes
```

### Merged and Unmerged Branches

```bash
# List branches merged into current branch
git branch --merged

# List branches NOT merged into current branch
git branch --no-merged

# List branches merged into specific branch
git branch --merged main

# List branches not merged into main
git branch --no-merged main
```

### Branch Tracking Information

```bash
# Show tracking branch relationships
git branch -vv

# Set upstream tracking for current branch
git branch --set-upstream-to=origin/main

# Set upstream when creating branch
git branch --track feature/auth origin/feature/auth

# Unset upstream tracking
git branch --unset-upstream
```

## Advanced Branch Operations

### Rename Branches

```bash
# Rename current branch
git branch -m new-name

# Rename specific branch
git branch -m old-name new-name

# Example: Rename master to main
git branch -m master main

# Update remote tracking after rename
git push origin -u new-name
git push origin --delete old-name
```

### Copy Branches

```bash
# Copy branch (create new branch pointing to same commit)
git branch -c existing-branch new-branch
git branch --copy existing-branch new-branch

# Copy current branch
git branch -c new-copy
```

### Force Operations

```bash
# Force create branch (overwrite if exists)
git branch -f feature/reset-point HEAD~3

# Force delete (even if unmerged)
git branch -D dangerous-experiment

# Force rename (overwrite target if exists)
git branch -M old-name new-name
```

## Remote Branch Management

### Tracking Remote Branches

```bash
# Create local branch tracking remote
git branch --track feature/auth origin/feature/auth

# Create and switch in one command
git checkout -b feature/auth origin/feature/auth
git switch -c feature/auth origin/feature/auth

# Set upstream for existing branch
git branch --set-upstream-to=origin/feature/auth feature/auth
git branch -u origin/feature/auth feature/auth
```

### Remote Branch Information

```bash
# List remote branches
git branch -r

# List all branches with remote info
git branch -a

# Show which remote branches are stale
git remote prune origin --dry-run

# Remove tracking branches for deleted remotes
git remote prune origin
```

## Filtering and Searching

### Pattern Matching

```bash
# List branches matching pattern
git branch --list "feature/*"
git branch --list "*auth*"

# Case-insensitive pattern matching
git branch --list "FEATURE/*" --ignore-case

# Use with other options
git branch -r --list "origin/release/*"
```

### Sort Options

```bash
# Sort by commit date (newest first)
git branch --sort=-committerdate

# Sort by author date
git branch --sort=-authordate

# Sort by version (useful for release branches)
git branch --sort=version:refname

# Multiple sort keys
git branch --sort=-committerdate --sort=objectname
```

### Filtering by Commit

```bash
# Branches containing specific commit
git branch --contains 1a2b3c4

# Branches not containing specific commit
git branch --no-contains 1a2b3c4

# Branches merged since specific commit
git branch --merged 1a2b3c4

# Branches pointing at specific commit
git branch --points-at HEAD~2
```

## Practical Workflows

### Feature Development Workflow

```bash
# Start new feature
git branch feature/user-profile
git switch feature/user-profile

# Or create and switch in one command
git switch -c feature/user-profile

# Work on feature, make commits...
git add .
git commit -m "Implement user profile display"

# Check if main has updates
git branch --merged main

# Finish feature
git switch main
git pull origin main
git merge feature/user-profile
git push origin main
git branch -d feature/user-profile
```

### Release Branch Workflow

```bash
# Create release branch from develop
git branch release/v2.1.0 develop

# Switch to release branch
git switch release/v2.1.0

# Make release preparations (version bumps, bug fixes)
git commit -am "Bump version to 2.1.0"

# Merge to main for release
git switch main
git merge release/v2.1.0
git tag v2.1.0

# Merge back to develop
git switch develop
git merge release/v2.1.0

# Clean up
git branch -d release/v2.1.0
```

### Branch Cleanup Workflow

```bash
# See what's been merged
git branch --merged main

# Delete merged branches (excluding current and main)
git branch --merged main | grep -v "\\* \\|main" | xargs -n 1 git branch -d

# See unmerged branches
git branch --no-merged main

# Review unmerged branches before deciding to delete
git branch --no-merged main | while read branch; do
    echo "=== $branch ==="
    git log --oneline main..$branch
done
```

## Branch Naming Conventions

### Common Patterns

```bash
# Feature branches
git branch feature/user-authentication
git branch feature/payment-integration
git branch feat/shopping-cart

# Bug fixes
git branch fix/login-redirect-bug
git branch bugfix/memory-leak
git branch hotfix/security-patch

# Releases
git branch release/v2.1.0
git branch release/2024-q1

# Experimental
git branch experiment/new-ui
git branch spike/performance-test
git branch prototype/ml-integration
```

### Team Conventions

```bash
# Include developer name for personal branches
git branch john/experiment-feature
git branch jane/prototype-idea

# Include ticket numbers
git branch feature/JIRA-123-user-auth
git branch fix/GH-456-memory-leak

# Date-based branches
git branch hotfix/2024-01-15-security
git branch release/2024-q1-features
```

## Automation and Scripting

### Branch Management Scripts

```bash
#!/bin/bash
# Clean up merged branches

# Get current branch
current_branch=$(git branch --show-current)

# Delete merged branches except current and main/master
git branch --merged | grep -vE "^\*|main|master|develop" | while read branch; do
    echo "Deleting merged branch: $branch"
    git branch -d "$branch"
done

echo "Branch cleanup complete"
```

### Branch Information Scripts

```bash
#!/bin/bash
# Show branch statistics

echo "=== Branch Summary ==="
echo "Total branches: $(git branch | wc -l)"
echo "Remote branches: $(git branch -r | wc -l)"
echo "Merged branches: $(git branch --merged | wc -l)"
echo "Unmerged branches: $(git branch --no-merged | wc -l)"

echo -e "\n=== Recent Activity ==="
git for-each-ref --format='%(refname:short) %(committerdate)' refs/heads | sort -k2 -r | head -10
```

## Branch Configuration

### Global Branch Settings

```bash
# Set default branch name for new repositories
git config --global init.defaultBranch main

# Always setup tracking when pushing new branches
git config --global push.autoSetupRemote true

# Set default merge strategy
git config --global branch.main.mergeOptions "--no-ff"
```

### Per-Branch Configuration

```bash
# Set merge strategy for specific branch
git config branch.develop.mergeoptions "--no-ff"

# Set rebase strategy for pulls
git config branch.feature/auth.rebase true

# Set push destination
git config branch.main.pushRemote origin
```

## Troubleshooting

### Common Branch Issues

```bash
# Branch doesn't exist
git branch non-existent
# error: branch 'non-existent' not found

# Can't delete current branch
git branch -d main  # while on main
# error: Cannot delete branch 'main' checked out at '/path/to/repo'

# Solution: Switch to different branch first
git switch other-branch
git branch -d main
```

### Recovery Operations

```bash
# Recover deleted branch (if you know last commit)
git branch recovered-branch 1a2b3c4

# Find recently deleted branch commits
git reflog | grep "branch-name"

# Recreate branch from reflog
git branch recovered-branch HEAD@{5}
```

### Synchronization Issues

```bash
# Remote branch exists but local doesn't track it
git branch --track local-name origin/remote-name

# Local branch exists but no upstream
git branch --set-upstream-to=origin/branch-name

# Upstream branch was deleted
git branch --unset-upstream
```

## Performance Tips

### Large Repository Optimization

```bash
# Limit branch listing in large repos
git branch | head -20

# Use patterns to narrow down
git branch --list "feature/2024*"

# Sort by recent activity
git branch --sort=-committerdate | head -10
```

## Examples

```bash
# Basic branch management
git branch                              # List branches
git branch feature/new-auth            # Create branch
git branch -d completed-feature        # Delete merged branch

# Information and filtering
git branch -v                          # Show last commit per branch
git branch --merged                    # Show merged branches
git branch --contains 1a2b3c4          # Branches containing commit

# Remote branch operations
git branch -r                          # List remote branches
git branch --track local origin/remote # Track remote branch
git branch --set-upstream-to=origin/main # Set upstream

# Advanced operations
git branch --sort=-committerdate       # Sort by date
git branch --list "feature/*"          # Pattern matching
git branch -m old-name new-name        # Rename branch
```


## Related Notes

- [[git-switch]] - Modern branch switching
- [[git-checkout]] - Legacy branch operations
- [[git-merge]] - Combine branches
- [[git-rebase]] - Reapply commits
- [[Branch]] - Understanding branch concepts
