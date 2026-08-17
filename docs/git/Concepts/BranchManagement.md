---
id: BranchManagement
aliases: []
tags: []
---

# Branch Management

## Advanced Branch Operations

### Branch Tracking

```bash
# Set upstream tracking
git push -u origin feature-branch

# Check tracking relationships
git branch -vv

# Set tracking for existing branch
git branch --set-upstream-to=origin/feature-branch
```

### Branch Comparison

```bash
# Compare branches
git diff main..feature-branch

# See commits in feature not in main
git log main..feature-branch

# See commits in both branches
git log main...feature-branch

# Files changed between branches
git diff --name-only main..feature-branch
```

### Branch Merging

```bash
# Fast-forward merge (if possible)
git merge feature-branch

# Always create merge commit
git merge --no-ff feature-branch

# Squash merge (combine all commits)
git merge --squash feature-branch
```

### Branch Rebasing

```bash
# Rebase feature onto main
git switch feature-branch
git rebase main

# Interactive rebase to clean history
git rebase -i HEAD~3

# Rebase and push
git push --force-with-lease origin feature-branch
```

## Branch Protection

### Local Protection

- Never work directly on main
- Always create feature branches
- Use pull requests for code review
- Protect against accidental pushes

### Remote Protection

- Branch protection rules
- Require pull request reviews
- Require status checks
- Restrict who can push

## Common Branch Patterns

### Short-lived Branches

- Created for specific features/fixes
- Deleted after merging
- Keep repository clean
- Easy to track progress

### Long-lived Branches

- main/master for production
- develop for integration
- release branches for versions
- Require more coordination

### Personal Branches

- Individual developer workspaces
- Experimentation and prototyping
- Not shared with team
- Freedom to rewrite history

## Branch Best Practices

### Creation

- Create from up-to-date main
- Use descriptive names
- One feature per branch
- Keep branches small and focused

### Development

- Commit frequently
- Write good commit messages
- Keep branch synchronized with main
- Test thoroughly before merging

### Cleanup

- Delete merged branches
- Regular branch maintenance
- Remove stale remote branches
- Keep active branch list manageable

## Troubleshooting Branches

### Common Issues

- [[DetachedHead]] - Not on any branch
- [[MergeConflicts]] - Conflicting changes
- [[LostCommits]] - Commits not on any branch
- Branch ahead/behind remote

### Recovery

```bash
# Create branch from detached HEAD
git switch -c recovery-branch

# Find lost commits
git reflog
git branch recovery-branch <commit-hash>

# Reset branch to specific state
git reset --hard origin/main
```

## Branch Visualization

### Command Line

```bash
# Graph view of branches
git log --graph --oneline --all

# Show branch relationships
git show-branch

# ASCII graph
git log --graph --pretty=oneline --abbrev-commit
```

### GUI Tools

- GitKraken
- SourceTree
- Git Extensions
- IDE integrations

## Related Notes

- [[Branch]] — Core concepts
- [[BranchManagement]] — This note
