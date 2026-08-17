---
id: StateTransitionsAndPatterns
aliases: []
tags: []
---

# State Transitions & Patterns

## State Transitions

### From Modified to Staged

```bash
git add <file>          # Specific file
git add .               # All changes in current directory
git add -A              # All changes in repository
git add -u              # All tracked files
git add *.js            # Pattern matching
```

### From Staged to Committed

```bash
git commit -m "message"     # With inline message
git commit                  # Opens editor for message
git commit --amend          # Modify last commit
git commit -v               # Show diff in commit message editor
```

### Backward Transitions

```bash
# Committed back to Modified (soft reset)
git reset --soft HEAD~1

# Staged back to Modified
git restore --staged <file>
git reset HEAD <file>       # Legacy syntax

# Modified back to last Committed state
git restore <file>
git checkout -- <file>     # Legacy syntax
```

## State Checking Commands

### Comprehensive Status Check

```bash
# Full status
git status

# Short format
git status -s
# ?? = untracked
# A  = added (new file staged)
# M  = modified (staged)
#  M = modified (not staged)
# MM = modified, staged, then modified again
# D  = deleted (staged)
#  D = deleted (not staged)
```

### State-Specific Diffs

```bash
# Working Directory vs Staging Area
git diff

# Staging Area vs Last Commit
git diff --staged

# Working Directory vs Last Commit
git diff HEAD

# Working Directory vs Specific Commit
git diff HEAD~2
```

## Best Practices for Three States

### Daily Workflow

1. **Start Clean**: `git status` should show clean working tree
2. **Make Changes**: Edit files in working directory
3. **Review Changes**: Use `git diff` to see what changed
4. **Stage Selectively**: Add related changes together
5. **Review Staged**: Use `git diff --staged` before committing
6. **Commit Atomically**: One logical change per commit
7. **Verify**: Check `git status` shows clean state

### Staging Strategy

- Stage related changes together
- Use interactive staging for large changes
- Review staged changes before committing
- Don't stage debugging code or temporary changes

### Commit Strategy

- Commit frequently with meaningful messages
- Each commit should be a working state
- Test before committing when possible
- Use `git commit --amend` for small fixes to last commit

## Common Three-State Patterns

### Feature Development

```bash
# Clean slate
git status  # clean

# Implement feature
# ... edit files ...

# Stage related changes
git add feature-files

# Commit feature
git commit -m "Implement user authentication"

# Continue with next part
# ... edit more files ...
git add additional-files
git commit -m "Add authentication middleware"
```

### Bug Fix Workflow

```bash
# Identify bug
git status  # clean

# Fix bug
# ... edit files ...

# Stage fix
git add buggy-file.js

# Commit fix
git commit -m "Fix null pointer exception in user login"

# Add test for bug
# ... edit test files ...
git add test-file.js
git commit -m "Add test for login null pointer bug"
```

### Experimental Changes

```bash
# Save current work
git add .
git commit -m "Save work in progress"

# Experiment
# ... make experimental changes ...

# If experiment succeeds
git add .
git commit -m "Implement experimental feature"

# If experiment fails
git restore .  # Discard changes
# Or
git stash     # Save for later
```

## Troubleshooting Three-State Issues

### Accidentally Staged Wrong Files

```bash
# Unstage specific file
git restore --staged wrong-file.txt

# Unstage everything and start over
git restore --staged .
git add correct-files
```

### Forgot to Stage Files Before Commit

```bash
# Add forgotten files to last commit
git add forgotten-file.txt
git commit --amend --no-edit
```

### Need to Split Large Commit

```bash
# Reset last commit but keep changes
git reset --soft HEAD~1

# Now files are staged - unstage and stage selectively
git restore --staged .
git add part1-files
git commit -m "Part 1: implement core functionality"

git add part2-files
git commit -m "Part 2: add error handling"
```

## Related Notes

- [[TheThreeStates]] — Core concepts
- [[StateTransitionsAndPatterns]] — This note
