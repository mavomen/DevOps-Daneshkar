---
id: git-switch
aliases: []
tags: []
---

# git switch

Switch between branches or restore working tree files. Modern Git command introduced in version 2.23 for clearer branch operations.

## Syntax

```bash
git switch [<options>] [<branch>]
git switch [<options>] --create <new-branch> [<start-point>]
git switch [<options>] --detach [<commit>]
```

## Description

The `git switch` command was introduced to provide a clearer alternative to `git checkout` for branch switching operations. It focuses specifically on switching [[Branch]]es and doesn't handle file restoration (use [[git-restore]] for that).

## Basic Usage

### Switch to Existing Branch

```bash
# Switch to existing branch
git switch main
git switch feature/user-auth
git switch release/v2.0

# Switch to previous branch
git switch -

# Switch using tab completion
git switch <TAB>  # Shows available branches
```

### Create and Switch to New Branch

```bash
# Create new branch and switch to it
git switch -c feature/new-payment
git switch --create feature/new-payment

# Create from specific starting point
git switch -c hotfix/bug-123 main
git switch -c feature/auth v1.0.0

# Create from another branch
git switch -c feature/enhancement feature/base
```

### Force Switch

```bash
# Force switch (discard uncommitted changes)
git switch --force main
git switch -f main

# Force create branch (overwrite if exists)
git switch -C feature/reset
git switch --force-create feature/reset
```

## Advanced Options

### Detached HEAD Operations

```bash
# Switch to specific commit (detached HEAD)
git switch --detach 1a2b3c4
git switch -d 1a2b3c4

# Switch to tag (detached HEAD)
git switch --detach v1.0.0

# Create branch from detached state
git switch --detach HEAD~3
git switch -c recovery-branch  # Create branch from detached state
```

### Remote Branch Operations

```bash
# Switch to remote branch (creates local tracking branch)
git switch origin/feature/auth

# Create local branch tracking remote
git switch -c local-feature origin/feature/remote-feature

# Switch to remote branch with different local name
git switch -c my-feature origin/team-feature
```

### Working Directory Control

```bash
# Discard uncommitted changes when switching
git switch --discard-changes main

# Merge uncommitted changes with target branch
git switch --merge main

# Keep changes in working directory (may cause conflicts)
git switch --ignore-other-worktrees main
```

## Branch Creation Options

### Create with Tracking

```bash
# Create branch tracking remote
git switch -c feature/auth --track origin/feature/auth

# Create without tracking (default for local branches)
git switch -c feature/local --no-track

# Let Git guess the remote branch
git switch -c auth  # If origin/auth exists, will track it
```

### Create from Specific Points

```bash
# Create from specific commit
git switch -c hotfix/patch 1a2b3c4

# Create from tag
git switch -c release/v2.1 v2.0.0

# Create from remote branch
git switch -c local-copy origin/experimental

# Create from another branch
git switch -c feature/v2 feature/v1
```

## Safety Features

### Uncommitted Changes Protection

```bash
# Git prevents switching if changes would be lost
echo "changes" >> important-file.txt
git switch main
# error: Your local changes to the following files would be overwritten by checkout:
#     important-file.txt
# Please commit your changes or stash them before you switch branches.

# Solutions:
# 1. Commit changes
git add important-file.txt
git commit -m "Work in progress"

# 2. Stash changes
git stash
git switch main
git stash pop  # When you return

# 3. Force switch (loses changes)
git switch --discard-changes main
```

### Untracked Files Warning

```bash
# Create untracked file
echo "content" > new-file.txt
git switch other-branch
# Switched to branch 'other-branch'
# (untracked files are carried over)

# If untracked file would conflict:
git switch conflict-branch
# error: The following untracked working tree files would be overwritten by checkout:
#     new-file.txt
# Please move or remove them before you switch branches.
```

## Practical Workflows

### Feature Development Workflow

```bash
# Start new feature from main
git switch main
git pull origin main
git switch -c feature/user-dashboard

# Work on feature
# ... make changes, commit ...

# Switch back to main for urgent fix
git switch main
git switch -c hotfix/critical-bug
# ... fix bug, commit ...

# Return to feature work
git switch feature/user-dashboard

# Finish feature
git switch main
git merge feature/user-dashboard
```

### Release Branch Workflow

```bash
# Prepare release
git switch develop
git pull origin develop
git switch -c release/v1.2.0

# Make release preparations
# ... version updates, changelog ...

# Merge to main
git switch main
git merge release/v1.2.0
git tag v1.2.0

# Merge back to develop
git switch develop
git merge release/v1.2.0

# Clean up
git branch -d release/v1.2.0
```

### Experimental Development

```bash
# Create experimental branch
git switch -c experiment/new-approach main

# Try experimental changes
# ... make risky changes ...

# If experiment works
git switch main
git merge experiment/new-approach

# If experiment fails
git switch main
git branch -D experiment/new-approach  # Force delete
```

### Quick Context Switching

```bash
# Working on feature A
git switch feature/auth-system
# ... working ...

# Need to check something on main
git stash  # Save work
git switch main
# ... investigate ...

# Back to feature work
git switch feature/auth-system
git stash pop  # Restore work

# Or use git switch - to go back
git switch -  # Returns to previous branch
```

## Integration with Remote Branches

### Automatic Remote Tracking

```bash
# If remote branch exists, git switch automatically tracks it
git fetch origin
git switch feature/remote-work  # Creates local branch tracking origin/feature/remote-work

# Explicit remote branch creation
git switch -c feature/local origin/feature/remote

# Create branch without remote
git switch -c feature/local-only  # No tracking setup
```

### Working with Forks

```bash
# Add upstream remote
git remote add upstream https://github.com/original/repo.git
git fetch upstream

# Switch to upstream branch
git switch -c feature/upstream-fix upstream/main

# Switch between your fork and upstream
git switch main  # Your fork's main
git switch upstream-main  # Create from upstream/main
```

## Error Handling and Recovery

### Common Switch Errors

```bash
# Branch doesn't exist
git switch non-existent-branch
# fatal: invalid reference: non-existent-branch

# Solution: Create it first
git switch -c non-existent-branch

# Or list available branches
git branch -a
```

### Resolving Conflicts During Switch

```bash
# If switching causes merge conflicts (with --merge option)
git switch --merge target-branch
# Auto-merging file.txt
# CONFLICT (content): Merge conflict in file.txt
# Switched to branch 'target-branch'

# Resolve conflicts manually
vim file.txt  # Edit conflict markers
git add file.txt
git commit -m "Resolve conflicts from branch switch"
```

### Recovery from Detached HEAD

```bash
# Accidentally in detached HEAD
git switch --detach 1a2b3c4
# ... make commits ...

# Create branch to save work
git switch -c recovery-branch

# Or switch back to a regular branch
git switch main  # Commits in detached HEAD become unreachable
```

## Performance Considerations

### Large Repository Optimization

```bash
# Switch with minimal working directory updates
git switch --quiet main

# Sparse checkout (only update specific paths)
git sparse-checkout set src/ docs/
git switch feature/docs-only  # Only updates tracked paths
```

### Network Operations

```bash
# Fetch before switching to remote branches
git fetch origin
git switch origin/feature/remote

# Or let switch fetch automatically (if configured)
git config --global remote.origin.fetch "+refs/heads/*:refs/remotes/origin/*"
```

## Configuration Options

### Switch Behavior Configuration

```bash
# Always create tracking branches for remote branches
git config --global branch.autosetupmerge always

# Set default behavior for new branches
git config --global push.autoSetupRemote true

# Configure switch to be more verbose
git config --global advice.detachedHead true
```

### Alias Configuration

```bash
# Useful git switch aliases
git config --global alias.sw switch
git config --global alias.swc "switch -c"
git config --global alias.swf "switch --force"

# Use aliases
git sw main           # git switch main
git swc new-feature   # git switch -c new-feature
git swf -c reset      # git switch --force-create reset
```

## Comparison with git checkout

### git switch vs git checkout

| Operation         | git switch             | git checkout           |
| ----------------- | ---------------------- | ---------------------- |
| **Switch branch** | `git switch main`      | `git checkout main`    |
| **Create branch** | `git switch -c new`    | `git checkout -b new`  |
| **Detached HEAD** | `git switch -d commit` | `git checkout commit`  |
| **Restore files** | ❌ Use `git restore`   | `git checkout -- file` |
| **Safety**        | ✅ Clearer intent      | ⚠️ Overloaded command  |

### Migration from git checkout

```bash
# Old git checkout usage
git checkout main                    # Switch branch
git checkout -b feature/new          # Create and switch
git checkout 1a2b3c4                # Detached HEAD
git checkout -- file.txt            # Restore file

# New git switch usage
git switch main                      # Switch branch
git switch -c feature/new            # Create and switch
git switch --detach 1a2b3c4         # Detached HEAD
git restore file.txt                # Restore file (different command)
```

## Best Practices

### Safe Switching Habits

1. **Check status first**: `git status` before switching
2. **Commit or stash**: Don't switch with uncommitted changes
3. **Use descriptive names**: Clear branch naming conventions
4. **Clean up regularly**: Delete merged branches
5. **Understand detached HEAD**: Know when you're in detached state

### Team Collaboration

```bash
# Sync before creating new branches
git switch main
git pull origin main
git switch -c feature/new-work

# Keep branches up to date
git switch feature/long-running
git merge main  # Or rebase main

# Clean branch naming for team
git switch -c feature/JIRA-123-user-auth
git switch -c hotfix/security-patch-2024-01
```

## Examples

```bash
# Basic branch switching
git switch main                       # Switch to main branch
git switch feature/auth              # Switch to feature branch
git switch -                         # Switch to previous branch

# Create and switch to new branches
git switch -c feature/payment        # Create and switch
git switch -c hotfix/bug main        # Create from main branch
git switch -c local origin/remote    # Create tracking remote

# Advanced operations
git switch --detach v1.0.0          # Switch to tag (detached)
git switch --force-create reset     # Force create branch
git switch --discard-changes main   # Switch discarding changes

# Working with remotes
git switch origin/feature/test       # Switch to remote branch
git switch -c my-copy origin/work    # Create local copy of remote
```


## Related Notes

- [[git-branch]] - Create and manage branches
- [[git-checkout]] - Legacy branch and file operations
- [[git-restore]] - Restore working tree files
- [[git-merge]] - Combine branch changes
- [[Branch]] - Understanding branch concepts
