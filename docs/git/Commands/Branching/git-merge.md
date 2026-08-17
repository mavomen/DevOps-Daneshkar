---
id: git-merge
aliases: []
tags: []
---

# git merge

Integrate changes from different branches by creating merge commits or performing fast-forward merges.

## Syntax

```bash
git merge [<options>] <commit>...
git merge [<options>] <msg> HEAD <commit>...
```

## Description

The `git merge` command combines the history of different [[Branch]]es into a single unified history. It's one of the primary methods for integrating changes in Git, alongside [[git-rebase]]. Merging preserves the context of parallel development and shows when features were integrated.

## Basic Usage

### Simple Merge

```bash
# Merge feature branch into current branch
git merge feature-branch

# Merge specific commit
git merge 1a2b3c4

# Merge with custom message
git merge feature-branch -m "Integrate user authentication feature"
```

### Fast-Forward Merge

```bash
# When target branch is direct descendant
git checkout main
git merge feature-branch

# Result: main pointer moves forward, no merge commit created
# Before:  main(A) <- feature(B)
# After:   main(B), feature(B)
```

### Three-Way Merge

```bash
# When branches have diverged
git checkout main
git merge feature-branch

# Result: new merge commit with two parents
# Before:  main(A-C), feature(A-B)
# After:   main(A-C-M), feature(A-B)
#          where M is merge commit with parents C and B
```

## Merge Options

### Merge Commit Control

```bash
# Always create merge commit (no fast-forward)
git merge --no-ff feature-branch

# Only allow fast-forward merges
git merge --ff-only feature-branch

# Default behavior (fast-forward when possible)
git merge feature-branch
```

### Commit Message Options

```bash
# Custom merge message
git merge -m "Merge feature: Add user authentication" feature-branch

# Edit merge message in editor
git merge --edit feature-branch

# No edit (use default message)
git merge --no-edit feature-branch

# Include merge request info in commit message
git merge -m "Merge pull request #123 from user/feature-branch" feature-branch
```

### Merge Strategies

```bash
# Recursive strategy (default for two branches)
git merge -s recursive feature-branch

# Octopus strategy (for multiple branches)
git merge -s octopus branch1 branch2 branch3

# Ours strategy (ignore other branch changes)
git merge -s ours old-branch

# Subtree strategy (for subproject merges)
git merge -s subtree -Xsubtree=lib/ library-branch
```

## Advanced Merge Options

### Strategy Options

```bash
# Favor our version in conflicts
git merge -X ours feature-branch

# Favor their version in conflicts
git merge -X theirs feature-branch

# Ignore whitespace changes
git merge -X ignore-space-change feature-branch

# Rename detection threshold
git merge -X rename-threshold=50 feature-branch

# Patience diff algorithm
git merge -X patience feature-branch
```

### Verification Options

```bash
# Verify signatures before merging
git merge --verify-signatures feature-branch

# Skip signature verification
git merge --no-verify-signatures feature-branch

# Require clean working directory
git merge --abort-on-dirty feature-branch
```

### Output Control

```bash
# Quiet merge (minimal output)
git merge --quiet feature-branch

# Verbose merge (detailed output)
git merge --verbose feature-branch

# Show merge progress
git merge --progress feature-branch

# No summary of merge
git merge --no-summary feature-branch
```

## Merge Conflicts

### Understanding Conflicts

Conflicts occur when the same lines are modified in both branches:

```bash
# File content during conflict:
<<<<<<< HEAD
function authenticate(user) {
    return validateWithJWT(user);
=======
function authenticate(user) {
    return validateWithOAuth(user);
>>>>>>> feature-branch
}
```

### Conflict Resolution Process

```bash
# 1. Merge attempts and fails with conflicts
git merge feature-branch
# Auto-merging auth.js
# CONFLICT (content): Merge conflict in auth.js
# Automatic merge failed; fix conflicts and then commit the result.

# 2. Check which files have conflicts
git status
# On branch main
# You have unmerged paths.
# Unmerged paths:
#   both modified:   auth.js

# 3. Edit files to resolve conflicts
vim auth.js  # Remove conflict markers and choose resolution

# 4. Mark conflicts as resolved
git add auth.js

# 5. Complete the merge
git commit  # Creates merge commit
```

### Conflict Resolution Tools

```bash
# Use configured merge tool
git mergetool

# Use specific merge tool
git mergetool --tool=vimdiff
git mergetool --tool=meld

# Manual resolution helpers
git checkout --ours auth.js    # Keep our version
git checkout --theirs auth.js  # Use their version
git checkout --merge auth.js   # Restore conflict markers
```

## Aborting and Continuing Merges

### Abort Merge

```bash
# Abort merge and return to pre-merge state
git merge --abort

# Equivalent older method
git reset --merge HEAD
```

### Continue After Resolving Conflicts

```bash
# After resolving all conflicts and staging files
git commit

# Or use merge continue (Git 2.12+)
git merge --continue
```

### Check Merge Status

```bash
# During merge, check status
git status

# See remaining conflicts
git diff

# See what's already staged
git diff --staged
```

## Merge Workflows

### Feature Branch Workflow

```bash
# Complete feature branch workflow
git checkout main
git pull origin main                # Get latest changes

git checkout feature/user-auth
git rebase main                     # Optional: rebase for linear history

git checkout main
git merge feature/user-auth         # Merge feature
git push origin main                # Share changes
git branch -d feature/user-auth     # Clean up
```

### Release Branch Workflow

```bash
# Merge release to main and back to develop
git checkout main
git merge release/v2.1.0
git tag v2.1.0

git checkout develop
git merge release/v2.1.0           # Merge back to develop
git branch -d release/v2.1.0       # Clean up release branch
```

### Hotfix Workflow

```bash
# Create hotfix from main
git checkout main
git checkout -b hotfix/critical-bug
# ... fix bug ...
git add .
git commit -m "Fix critical security vulnerability"

# Merge hotfix to main
git checkout main
git merge hotfix/critical-bug
git tag v1.2.1

# Merge hotfix to develop
git checkout develop
git merge hotfix/critical-bug
git branch -d hotfix/critical-bug
```

### Multiple Feature Integration

```bash
# Integrate multiple completed features
git checkout develop

git merge feature/auth-system       # Merge first feature
git merge feature/payment-gateway   # Merge second feature
git merge feature/user-dashboard     # Merge third feature

# Test integration
# ... run tests ...

# If integration successful, merge to main
git checkout main
git merge develop
```

## Merge Commit Best Practices

### Good Merge Messages

```bash
# Descriptive merge messages
git merge -m "Merge feature/user-auth: Add JWT authentication system

- Implement login/logout functionality
- Add password hashing with bcrypt
- Create authentication middleware
- Add comprehensive test coverage
- Update API documentation

Resolves: #123, #124" feature/user-auth

# Include relevant information
git merge -m "Merge hotfix/security-patch

Critical security fix for XSS vulnerability
in user input validation.

Affects: All versions since v1.0.0
Testing: Manual testing and security scan completed" hotfix/security
```

### Merge Commit Structure

```bash
# Standard format for merge commits
# First line: Brief summary of what's being merged
# Blank line
# Detailed description of changes
# References to issues/PRs
# Testing notes
# Breaking changes (if any)
```

## Merge vs Rebase Decision

### Use Merge When:

- Preserving branch history is important
- Working on shared/public branches
- Complex feature integration with multiple developers
- Want to maintain context of feature development

### Use Rebase When:

- Want linear project history
- Working on personal feature branches
- Simple feature with clean commit history
- Preparing for merge into main branch

### Example Comparison:

```bash
# Merge preserves branch structure
git checkout main
git merge feature/auth
# Result: Shows when feature was developed in parallel

# Rebase creates linear history
git checkout feature/auth
git rebase main
git checkout main
git merge feature/auth  # Fast-forward merge
# Result: Looks like feature was developed on latest main
```

## Advanced Merge Scenarios

### Octopus Merge (Multiple Branches)

```bash
# Merge multiple branches simultaneously
git merge feature/auth feature/payment feature/ui

# Useful for integrating multiple completed features
git checkout integration-branch
git merge feature-a feature-b feature-c
```

### Subtree Merge (Subproject Integration)

```bash
# Merge external project as subtree
git remote add library https://github.com/user/library.git
git fetch library
git merge -s subtree --no-commit library/main
git commit -m "Integrate library as subtree"
```

### Cherry-pick vs Merge

```bash
# Cherry-pick: Apply specific commits
git cherry-pick 1a2b3c4 5d6e7f8

# Merge: Integrate entire branch history
git merge feature-branch

# Use cherry-pick for selective changes
# Use merge for complete feature integration
```

## Merge Conflict Resolution Strategies

### Automated Resolution

```bash
# Prefer our version for all conflicts
git merge -X ours feature-branch

# Prefer their version for all conflicts
git merge -X theirs feature-branch

# Combine with manual resolution for specific files
git merge feature-branch
git checkout --ours problematic-file.js
git checkout --theirs good-file.css
git add .
git commit
```

### Complex Conflict Resolution

```bash
# For complex conflicts, use temporary branches
git checkout -b merge-resolution main
git merge feature-branch

# Resolve conflicts carefully
# ... manual resolution ...

# Test resolution
# ... run tests ...

# Apply to main
git checkout main
git merge merge-resolution
git branch -d merge-resolution
```

### File-Specific Merge Strategies

```bash
# Configure merge driver for specific files
echo "*.generated merge=ours" >> .gitattributes
git config merge.ours.driver true

# Custom merge drivers
git config merge.custom.driver 'custom-merge-tool %O %A %B %L'
echo "*.xml merge=custom" >> .gitattributes
```

## Troubleshooting Merges

### Common Merge Issues

```bash
# Merge refuses to start
git merge feature-branch
# error: Entry 'file.txt' would be overwritten by merge

# Solutions:
git status                  # Check working directory state
git stash                  # Save uncommitted changes
git commit -am "Save WIP"  # Commit changes
```

### Post-Merge Issues

```bash
# Wrong files merged
git reset --hard HEAD~1    # Undo merge (if not pushed)
git revert -m 1 HEAD       # Revert merge (safe for shared branches)

# Merge created wrong result
git checkout main
git reset --hard ORIG_HEAD  # Reset to pre-merge state
```

### Performance Issues

```bash
# Large merge taking too long
git config merge.tool patience
git config merge.renameLimit 1000

# Resume interrupted merge
git status
git add resolved-files
git commit
```

## Examples

```bash
# Basic merge operations
git merge feature-branch              # Simple merge
git merge --no-ff feature-branch      # Force merge commit
git merge --ff-only feature-branch    # Only if fast-forward possible

# Merge with custom message
git merge -m "Integrate auth system" feature/auth

# Handle conflicts
git merge feature-branch              # Conflicts occur
git status                           # Check conflicted files
# ... resolve conflicts ...
git add .                            # Stage resolved files
git commit                           # Complete merge

# Advanced merge strategies
git merge -X ours feature-branch      # Favor our changes
git merge -s recursive -X patience feature-branch  # Use patience algorithm

# Multiple branch merge
git merge feature-a feature-b feature-c  # Octopus merge

# Abort and retry
git merge feature-branch              # Start merge
git merge --abort                     # Cancel if problems
```


## Related Notes

- [[git-rebase]] - Alternative integration method
- [[git-cherry-pick]] - Selective commit application
- [[git-revert]] - Undo merge commits
- [[MergeConflicts]] - Detailed conflict resolution
- [[Branch]] - Understanding branch concepts
