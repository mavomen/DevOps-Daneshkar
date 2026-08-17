---
id: MergeConflictResolution
aliases: []
tags: []
---

# Merge Conflict Resolution

## Conflict Types and Resolution

### Content Conflicts

```bash
# Same lines modified differently
<<<<<<< HEAD
const API_URL = "https://api.example.com";
=======
const API_URL = "https://api-v2.example.com";
>>>>>>> feature-branch

# Resolution: Choose one or combine
const API_URL = "https://api-v2.example.com";
```

### Add/Add Conflicts

```bash
# Both sides added same file with different content
# Both sides:
#   added: newfile.txt

# Git cannot automatically resolve
# Must manually choose content or combine
```

### Delete/Modify Conflicts

```bash
# One side deleted file, other modified it
# CONFLICT (modify/delete): file.txt deleted in HEAD and modified in feature-branch

# Choose resolution:
git rm file.txt              # Accept deletion
git add file.txt             # Keep modification
```

## Merge Tools and Automation

### Configuring Merge Tools

```bash
# Set up visual merge tool
git config merge.tool vimdiff
git config merge.tool meld
git config merge.tool vscode

# Configure custom merge tool
git config merge.tool custom
git config mergetool.custom.cmd 'my-merge-tool $BASE $LOCAL $REMOTE $MERGED'
```

### Using Merge Tools

```bash
# Launch merge tool during conflict
git mergetool

# Merge tool shows three panes:
# - Local (ours)
# - Base (common ancestor)
# - Remote (theirs)
# - Result (merged output)
```

### Automated Conflict Resolution

```bash
# Favor our side for all conflicts
git merge -X ours feature-branch

# Favor their side for all conflicts
git merge -X theirs feature-branch

# Custom resolution scripts
git config merge.driver.command 'custom-merge-script %O %A %B %L'
```

## Best Practices for Three-Way Merges

### Before Merging

```bash
# 1. Ensure working directory is clean
git status

# 2. Update both branches
git checkout main && git pull
git checkout feature-branch && git rebase main

# 3. Review changes to be merged
git diff main..feature-branch

# 4. Consider merge strategy
git merge --no-commit feature-branch  # Preview merge
git merge --abort                     # Cancel preview
```

### During Conflicts

```bash
# 1. Understand the conflict context
git log --merge                 # Show conflicting commits
git diff                       # Show current conflicts

# 2. Resolve conflicts thoughtfully
# - Consider intent of both changes
# - Test resolution thoroughly
# - Document complex resolutions

# 3. Verify resolution
git diff --staged              # Check staged resolution
```

### After Merging

```bash
# 1. Test merged result
# - Run tests
# - Manual verification
# - Check for integration issues

# 2. Write descriptive merge commit message
git commit -v                  # Show diff in commit message

# 3. Clean up branches if appropriate
git branch -d feature-branch
```

## Merge Commit Messages

### Good Merge Commit Messages

```bash
# Descriptive merge messages
git commit -m "Merge branch 'feature/user-authentication'

Integrates JWT-based authentication system:
- Add login/logout functionality
- Implement password hashing
- Create authentication middleware
- Add comprehensive test coverage

Resolves conflicts in:
- config/auth.js: Combined timeout settings
- src/middleware.js: Integrated error handling

Closes #123"
```

### Merge Message Templates

```bash
# Configure merge message template
git config commit.template ~/.gitmessage

# Template file:
# Merge branch 'BRANCH_NAME'
#
# Brief description of what's being merged
#
# Conflicts resolved:
# - file1: description of resolution
# - file2: description of resolution
#
# Testing:
# - Description of testing performed
#
# References: #issue-numbers
```

## Performance and Optimization

### Large Repository Merges

```bash
# Configure merge performance
git config merge.renameLimit 1000
git config diff.renameLimit 1000

# Use faster merge strategies
git config merge.tool patience

# Parallel processing
git config merge.parallel 4
```

### Reducing Merge Conflicts

```bash
# Strategies to minimize conflicts:
# 1. Frequent integration
git rebase main                # Keep feature branch current

# 2. Modular development
# - Small, focused changes
# - Clear separation of concerns

# 3. Communication
# - Coordinate overlapping work
# - Share work-in-progress

# 4. Code organization
# - Avoid large files
# - Use consistent formatting
```

## Troubleshooting Three-Way Merges

### Common Issues

```bash
# Merge conflicts seem wrong
git rerere status              # Check rerere state
git rerere diff               # Show rerere resolutions

# Merge took wrong files
git show --stat               # Check what was merged
git reset --hard ORIG_HEAD    # Undo merge (if not pushed)

# Merge performance issues
git config merge.renameLimit 0  # Disable rename detection
git config core.precomposeunicode true  # Unicode issues
```

### Recovery Techniques

```bash
# Undo problematic merge
git reset --hard HEAD~1       # Remove merge commit (local only)
git revert -m 1 HEAD          # Revert merge (safe for shared)

# Re-attempt merge with different strategy
git merge -s resolve feature-branch
git merge -X patience feature-branch
```

## Related Notes

- [[ThreeWayMerge]] — Core concepts
- [[MergeConflictResolution]] — This note
