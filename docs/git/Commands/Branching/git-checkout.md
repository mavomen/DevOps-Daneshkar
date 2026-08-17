---
id: git-checkout
aliases: []
tags: []
---

# git checkout

Switch branches, restore files, or create branches. The original multipurpose command that's being superseded by more specific commands like `git switch` and `git restore`.

## Syntax

```bash
git checkout [<options>] <branch>
git checkout [<options>] [<branch>] -- <pathspec>...
git checkout [<options>] <commit>
```

## Description

The `git checkout` command is Git's original Swiss Army knife for branch switching and file restoration. While still widely used and fully supported, newer commands like [[git-switch]] (for branches) and [[git-restore]] (for files) provide clearer intent and safer operations.

## Branch Operations

### Switch Between Branches

```bash
# Switch to existing branch
git checkout main
git checkout feature/user-auth
git checkout release/v2.0

# Switch to previous branch
git checkout -

# Switch with explicit branch
git checkout --branch existing-branch
```

### Create and Switch to New Branch

```bash
# Create new branch and switch to it
git checkout -b feature/new-payment
git checkout -b hotfix/bug-123 main

# Create from specific commit
git checkout -b recovery-branch 1a2b3c4

# Create from tag
git checkout -b hotfix/v1.1.1 v1.1.0

# Create from remote branch
git checkout -b local-feature origin/remote-feature
```

### Force Operations

```bash
# Force switch (discard uncommitted changes)
git checkout -f main
git checkout --force main

# Force create branch (overwrite if exists)
git checkout -B feature/reset
git checkout --force-create feature/reset main
```

## File Restoration Operations

### Restore Files from Specific Commit

```bash
# Restore file from HEAD (last commit)
git checkout HEAD -- filename.txt

# Restore file from specific commit
git checkout 1a2b3c4 -- src/app.js

# Restore file from another branch
git checkout main -- config.json
git checkout feature/auth -- auth-module.js

# Restore file from tag
git checkout v1.0.0 -- legacy-config.xml
```

### Restore Multiple Files and Directories

```bash
# Restore all files in directory
git checkout HEAD -- src/

# Restore multiple files
git checkout HEAD -- file1.txt file2.js src/app.js

# Restore all changes (dangerous)
git checkout HEAD -- .

# Restore with patterns
git checkout HEAD -- '*.js'
git checkout HEAD -- 'src/**/*.css'
```

### Partial File Restoration

```bash
# Interactive patch mode
git checkout -p HEAD -- filename.txt
git checkout --patch HEAD~1 -- src/app.js

# Patch mode options:
# y - apply this hunk
# n - do not apply this hunk
# q - quit; do not apply this hunk or any remaining ones
# a - apply this hunk and all later hunks in the file
# d - do not apply this hunk or any later hunks in the file
# s - split the current hunk into smaller hunks
# e - manually edit the current hunk
```

## Detached HEAD Operations

### Switch to Specific Commit

```bash
# Checkout specific commit (detached HEAD)
git checkout 1a2b3c4

# Checkout with explicit detach
git checkout --detach 1a2b3c4

# Checkout tag (creates detached HEAD)
git checkout v1.0.0

# Checkout relative commit
git checkout HEAD~3
git checkout main~5
```

### Working in Detached HEAD

```bash
# Make changes in detached HEAD
git checkout 1a2b3c4
echo "experimental changes" > test.txt
git add test.txt
git commit -m "Experimental commit"

# Create branch to save work
git checkout -b experimental-feature

# Or return to branch (loses detached commits)
git checkout main  # Detached commits become unreachable
```

## Remote Branch Operations

### Checkout Remote Branches

```bash
# Checkout remote branch (creates local tracking branch)
git checkout origin/feature/remote-work

# Explicit tracking setup
git checkout -b local-name origin/remote-name
git checkout --track origin/feature/auth

# Checkout without tracking
git checkout --no-track -b local-copy origin/remote-branch
```

### Working with Multiple Remotes

```bash
# Checkout from specific remote
git checkout -b feature/upstream upstream/feature/new

# Checkout and set different upstream
git checkout -b feature/local origin/feature/remote
git branch --set-upstream-to=upstream/feature/remote
```

## Advanced Options

### Conflict Resolution Options

```bash
# Merge changes when switching branches
git checkout --merge target-branch

# Use specific merge strategy
git checkout -m --strategy=resolve target-branch

# Checkout and resolve conflicts in favor of specific side
git checkout --ours -- conflicted-file.txt    # Keep current branch version
git checkout --theirs -- conflicted-file.txt  # Use target branch version
```

### Working Directory Control

```bash
# Ignore unmerged entries
git checkout --ignore-unmerged main

# Overlay mode (default) - only update existing files
git checkout main

# No-overlay mode - update all files from target
git checkout --no-overlay main
```

### Path Limiting

```bash
# Checkout files matching pathspec
git checkout HEAD -- 'src/**/*.js'

# Exclude specific paths
git checkout HEAD -- . ':(exclude)*.log'

# Case-insensitive matching
git checkout HEAD -- ':(icase)*.LOG'

# Checkout from index (staged version)
git checkout --staged -- filename.txt
```

## Common Workflows

### Emergency File Recovery

```bash
# Accidentally deleted important file
git checkout HEAD -- important-file.txt

# Restore file from before recent changes
git checkout HEAD~1 -- damaged-file.js

# Get file from different branch
git checkout feature/working-version -- fixed-file.css
```

### Experimental Development

```bash
# Create experimental branch from specific commit
git checkout -b experiment/new-idea 1a2b3c4

# Try different implementation
git checkout -b experiment/alternative main

# Compare experiments
git checkout experiment/approach-a
git diff experiment/approach-b
```

### Partial File Updates

```bash
# Get specific configuration from another branch
git checkout production -- config/database.yml

# Update documentation from main
git checkout main -- README.md docs/

# Get latest version of specific module
git checkout origin/main -- src/auth-module/
```

### Release Preparation

```bash
# Create release branch
git checkout -b release/v2.1.0 develop

# Cherry-pick specific files from features
git checkout feature/critical-fix -- src/security-patch.js

# Get updated documentation
git checkout main -- CHANGELOG.md
```

## Safety Considerations

### Avoiding Data Loss

```bash
# Always check status before checkout
git status
git diff  # See what would be lost

# Stash changes before switching
git stash
git checkout other-branch
git stash pop  # When returning

# Commit work before risky operations
git add .
git commit -m "WIP: save before checkout experiment"
```

### Understanding Destructive Operations

```bash
# These operations can lose work:
git checkout HEAD -- .           # ⚠️  Discards ALL working directory changes
git checkout -f other-branch     # ⚠️  Forces switch, discards changes
git checkout --hard HEAD         # ❌ Invalid syntax (use git reset)

# Safer alternatives:
git stash                        # ✅ Save changes temporarily
git commit -m "WIP"              # ✅ Create checkpoint
git switch --discard-changes     # ✅ Explicit intent with new command
```

## Integration with Other Commands

### Working with git stash

```bash
# Stash and checkout workflow
git stash
git checkout other-branch
# ... work on other branch ...
git checkout -  # Return to previous branch
git stash pop
```

### Working with git worktree

```bash
# Instead of constant checkout, use worktrees
git worktree add ../feature-work feature/new-auth
cd ../feature-work
# Work without affecting main working directory
```

### Working with git bisect

```bash
# Checkout during bisect
git bisect start
git bisect bad HEAD
git bisect good v1.0.0

# Git automatically checkouts commits for testing
# After marking good/bad, git checks out next commit

git bisect reset  # Return to original branch
```

## Migration to Modern Commands

### Replacing with git switch

```bash
# Old checkout usage
git checkout main                    # Switch branch
git checkout -b feature/new          # Create and switch
git checkout -f other-branch         # Force switch

# Modern git switch equivalent
git switch main                      # Switch branch
git switch -c feature/new            # Create and switch
git switch --discard-changes other-branch  # Force switch
```

### Replacing with git restore

```bash
# Old checkout usage for files
git checkout HEAD -- file.txt       # Restore file
git checkout main -- file.txt       # Restore from branch
git checkout HEAD~1 -- file.txt     # Restore from commit

# Modern git restore equivalent
git restore file.txt                 # Restore file
git restore --source=main file.txt   # Restore from branch
git restore --source=HEAD~1 file.txt # Restore from commit
```

### When to Still Use git checkout

```bash
# Some operations still require checkout:
git checkout --patch HEAD -- file.txt    # Interactive file restoration
git checkout --ours -- file.txt          # Conflict resolution
git checkout --theirs -- file.txt        # Conflict resolution

# Complex pathspec operations
git checkout HEAD -- ':(exclude)*.log'
```

## Performance Considerations

### Large Repository Optimization

```bash
# Minimal checkout for large repos
git checkout --quiet main

# Sparse checkout
git config core.sparseCheckout true
echo "src/*" >> .git/info/sparse-checkout
git checkout main  # Only checks out src/ directory
```

### Network Operations

```bash
# Fetch before checking out remote branches
git fetch origin
git checkout origin/feature/remote

# Or combine operations
git fetch origin feature/remote:feature/local
git checkout feature/local
```

## Troubleshooting

### Common Checkout Errors

```bash
# Error: pathspec did not match any files
git checkout HEAD -- nonexistent.txt
# error: pathspec 'nonexistent.txt' did not match any file(s) known to git

# Error: Your local changes would be overwritten
git checkout main
# error: Your local changes would be overwritten by checkout

# Solutions:
git status                    # Check what changes exist
git stash                    # Save changes temporarily
git commit -m "Save work"    # Commit changes
git checkout -f main         # Force checkout (loses changes)
```

### Recovery Operations

```bash
# Accidentally discarded changes
git checkout HEAD -- important-file.txt  # Oops!

# Look for previous versions
git reflog
git log --oneline -p -- important-file.txt

# Restore from commit where file had content
git checkout 1a2b3c4 -- important-file.txt
```

### Detached HEAD Issues

```bash
# Stuck in detached HEAD with important commits
git log --oneline  # Find commit hashes
git checkout -b recovery-branch  # Create branch from current state

# Or merge commits into existing branch
git checkout main
git merge 1a2b3c4  # Merge specific detached HEAD commit
```

## Examples

```bash
# Branch operations
git checkout main                     # Switch to main branch
git checkout -b feature/auth          # Create and switch to new branch
git checkout -                       # Switch to previous branch

# File restoration
git checkout HEAD -- file.txt        # Restore file from last commit
git checkout main -- config.json     # Get file from main branch
git checkout HEAD~2 -- old-file.js   # Restore from 2 commits ago

# Detached HEAD operations
git checkout v1.0.0                  # Checkout tag (detached HEAD)
git checkout 1a2b3c4                 # Checkout specific commit
git checkout -b fix-branch           # Create branch from detached state

# Advanced file operations
git checkout --patch HEAD -- file.txt # Interactive restoration
git checkout --ours -- conflict.txt   # Resolve conflict (keep ours)
git checkout HEAD -- 'src/**/*.js'    # Restore all JS files in src/
```


## Related Notes

- [[git-switch]] - Modern branch switching
- [[git-restore]] - Modern file restoration
- [[git-branch]] - Branch management
- [[git-merge]] - Combine branches
- [[git-stash]] - Temporary change storage
