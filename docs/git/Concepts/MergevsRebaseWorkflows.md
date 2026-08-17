---
id: MergevsRebaseWorkflows
aliases: []
tags: []
---

# Merge vs Rebase Workflows

## Workflow Patterns

### GitHub Flow (Merge-Heavy)

```bash
# 1. Create feature branch
git checkout -b feature/user-profile

# 2. Develop feature (multiple commits)
git commit -m "Add user model"
git commit -m "Add profile controller"
git commit -m "Add profile views"

# 3. Open pull request
# 4. Code review process
# 5. Merge via GitHub interface (creates merge commit)
git checkout main
git pull origin main        # Contains merge commit
```

### Rebase Workflow (Linear History)

```bash
# 1. Create feature branch
git checkout -b feature/user-profile

# 2. Develop feature
git commit -m "Add user profile feature"

# 3. Before merging, update and clean
git rebase main             # Update with latest
git rebase -i main          # Clean up if needed

# 4. Merge (fast-forward)
git checkout main
git merge feature/user-profile  # Fast-forward merge
```

### Hybrid Approach

```bash
# Rebase for preparation, merge for integration
git checkout feature-branch
git rebase -i main          # Clean up personal commits
git checkout main
git merge --no-ff feature-branch  # Preserve integration context
```

## Advanced Considerations

### Git Bisect and History

### With Merge Commits

```bash
git bisect start
git bisect bad HEAD
git bisect good v1.0.0

# Bisect may land on merge commits
# Need to understand which parent introduced issue
git show --first-parent      # Show merge commit changes
```

### With Linear History

```bash
git bisect start
git bisect bad HEAD
git bisect good v1.0.0

# Cleaner bisect path
# Each step is a meaningful commit
# Easier to identify problematic change
```

### Team Coordination

### Merge-Friendly Teams

- Less Git expertise required
- Safer default operations
- Natural collaboration patterns
- Feature context preserved

### Rebase-Savvy Teams

- Higher Git expertise needed
- Cleaner project history
- More coordination required
- Better for linear workflows

### Repository Size and Performance

### Large Repositories

```bash
# Merge operations are generally faster
git merge feature-branch    # Single conflict resolution

# Rebase can be slower with many commits
git rebase main            # Multiple conflict opportunities
```

### Small, Active Projects

```bash
# Rebase keeps history clean and navigable
git rebase -i HEAD~10      # Easy to clean recent history
```

## Best Practices by Scenario

### Personal Development

```bash
# Use rebase freely for personal branches
git rebase -i HEAD~5       # Squash commits
git rebase main           # Update branch
git push --force-with-lease origin feature-branch
```

### Team Feature Development

```bash
# Use merge for team integration
git checkout main
git merge --no-ff feature/team-effort
git push origin main
```

### Open Source Contributions

```bash
# Clean up before submitting PR
git rebase -i upstream/main
git push --force-with-lease origin feature-branch
# Submit PR for review, maintainer merges
```

### Hotfix Deployment

```bash
# Merge for clear audit trail
git checkout main
git merge hotfix/security-patch
git tag v1.2.1
git push origin main --tags
```

## Common Anti-Patterns

### Avoid These Patterns

### 1. Rebasing Public Branches

```bash
# DON'T DO THIS
git checkout main           # Shared branch
git rebase feature-branch   # Rewrites shared history
git push --force origin main  # Destroys others' work
```

### 2. Unnecessary Merge Commits

```bash
# Avoid merge commits for simple updates
git checkout main
git pull origin main
git checkout feature-branch
git merge main              # Creates unnecessary merge commit

# Better: rebase to stay current
git rebase main
```

### 3. Complex Rebase on Shared Branches

```bash
# Don't rebase complex shared feature branches
git checkout shared-feature
git rebase -i main          # Others have this branch
git push --force origin shared-feature  # Breaks others' work
```

## Migration Strategies

### From Merge-Heavy to Rebase-Friendly

1. **Team Education**: Train team on rebase operations
2. **Gradual Introduction**: Start with personal branch rebases
3. **Clear Guidelines**: Document when to use each approach
4. **Tool Configuration**: Set up aliases and defaults

### From Chaotic to Structured

1. **Establish Conventions**: Decide on merge vs rebase policies
2. **Branch Protection**: Use branch protection rules
3. **Code Review**: Enforce clean history through reviews
4. **Automation**: Use tools to enforce standards

## Related Notes

- [[MergevsRebase]] — Core concepts
- [[MergevsRebaseWorkflows]] — This note
