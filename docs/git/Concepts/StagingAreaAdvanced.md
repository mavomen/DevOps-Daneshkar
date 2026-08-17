---
id: StagingAreaAdvanced
aliases: []
tags: []
---

# Staging Area Advanced

## Advanced Staging Techniques

### Interactive Staging

```bash
# Enter interactive mode
git add -i

# Interactive menu options:
# 1: status        - show paths with changes
# 2: update        - add working tree state to index
# 3: revert        - revert staged changes
# 4: add untracked - add untracked paths
# 5: patch         - pick hunks and update selectively
# 6: diff          - view diff between HEAD and index
# 7: quit          - quit interactive mode
```

### Patch Mode

```bash
# Stage by hunks
git add -p

# Edit hunks manually
git add -p
# Choose 'e' to edit hunk manually
# Remove lines you don't want to stage
```

### Intent to Add

```bash
# Track new file without staging content
git add -N newfile.txt

# Now you can see diff for new file
git diff newfile.txt

# Stage the content when ready
git add newfile.txt
```

## Staging Area Workflows

### Feature Development

```bash
# Start feature
git switch -c feature/user-auth

# Make multiple changes
# Edit auth.js, user.js, styles.css

# Stage related changes together
git add auth.js user.js
git commit -m "Add user authentication logic"

# Stage remaining changes
git add styles.css
git commit -m "Update styles for auth forms"
```

### Bug Fix Workflow

```bash
# Make emergency fix
git switch -c hotfix/security-patch

# Fix issue and add test
# Edit security.js, test-security.js

# Stage and review
git add security.js
git diff --staged  # Review security fix

git add test-security.js
git diff --staged  # Review complete fix

# Commit fix
git commit -m "Fix security vulnerability in auth"
```

### Refactoring Workflow

```bash
# Large refactoring with multiple logical changes

# Stage formatting changes first
git add -p  # Select only whitespace/formatting

git commit -m "Format code according to style guide"

# Stage logic changes
git add .
git commit -m "Refactor authentication logic"
```

## Common Staging Mistakes

### Staging Unintended Changes

```bash
# Problem: Accidentally staged debug code
git add .  # Oops, included debug statements

# Solution: Unstage and restage selectively
git restore --staged .
git add -p  # Choose only intended changes
```

### Forgetting to Stage

```bash
# Problem: Made changes but forgot to stage
git commit -m "Add feature"  # Nothing committed!

# Solution: Stage then commit
git add .
git commit -m "Add feature"
```

### Partial File Issues

```bash
# Problem: File has both staged and unstaged changes
# Want to commit only staged portion

# Solution: Commit staged, then continue with unstaged
git commit -m "Partial implementation"
git diff  # See remaining changes
```

## Staging Area Internals

### Where is the Staging Area?

- Stored in `.git/index` file
- Binary format containing file metadata
- Contains SHA hashes of staged file contents

### Viewing Index Contents

```bash
# Low-level view of staged files
git ls-files --stage

# Compare index with HEAD
git diff --cached

# Compare index with working directory
git diff
```

## Troubleshooting Staging Issues

### Index Lock Issues

```bash
# If staging operations fail
rm .git/index.lock

# Rebuild index if corrupted
git read-tree HEAD
git checkout-index -f -a
```

### Large Staging Operations

- Stage files in smaller batches
- Use `.gitignore` to exclude large files
- Consider Git LFS for large binary files

## Related Notes

- [[StagingArea]] — Core concepts
- [[StagingAreaAdvanced]] — This note
