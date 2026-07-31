---
id: git-commit
aliases: []
tags: []
---

# git commit

Create a snapshot of the staged changes and store it in the Git repository with a descriptive message.

## Syntax

```bash
git commit [<options>] [--] [<pathspec>...]
```

## Description

The `git commit` command creates a new [[Commit]] object that contains the changes currently in the [[StagingArea]]. Each commit represents a snapshot of your project at a specific point in time and includes metadata such as author, timestamp, and commit message.

## Basic Usage

### Simple Commit

```bash
# Commit staged changes with inline message
git commit -m "Add user authentication feature"

# Commit with multiline message
git commit -m "Add user authentication

- Implement login/logout functionality
- Add password hashing
- Create authentication middleware
- Add user session management"
```

### Commit with Editor

```bash
# Open default editor for commit message
git commit

# Editor opens with template:
#
# # Please enter the commit message for your changes. Lines starting
# # with '#' will be ignored, and an empty message aborts the commit.
# #
# # On branch main
# # Changes to be committed:
# #       new file:   auth.js
# #       modified:   app.js
# #
```

### Stage and Commit Together

```bash
# Stage all tracked files and commit
git commit -a -m "Update all existing files"
git commit -am "Quick update to existing files"

# Note: -a only stages modified/deleted tracked files, not new files
```

## Commit Options

### Amending Commits

```bash
# Modify the last commit
git commit --amend -m "Better commit message"

# Add forgotten files to last commit
git add forgotten-file.txt
git commit --amend --no-edit

# Change author of last commit
git commit --amend --author="New Author <new@email.com>"
```

### Message Options

```bash
# Commit with file as message source
git commit -F commit-message.txt

# Reuse message from another commit
git commit -C 1a2b3c4

# Edit message from another commit
git commit -c 1a2b3c4

# Use template file
git commit -t ~/.gitmessage.txt
```

### Signing Commits

```bash
# Sign commit with GPG key
git commit -S -m "Signed commit"

# Sign and use configured signing key
git commit --gpg-sign=KEYID -m "Commit with specific key"

# Skip signing (if gpg.sign is enabled globally)
git commit --no-gpg-sign -m "Unsigned commit"
```

### Special Commit Types

```bash
# Allow empty commit (no staged changes)
git commit --allow-empty -m "Trigger CI build"

# Allow commit with empty message
git commit --allow-empty-message

# Include untracked files in commit message template
git commit --untracked-files
```

## Commit Message Best Practices

### Message Structure

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Conventional Commits

```bash
# Feature addition
git commit -m "feat(auth): add JWT token authentication"

# Bug fix
git commit -m "fix(ui): resolve button alignment issues"

# Documentation
git commit -m "docs(api): update endpoint documentation"

# Code refactoring
git commit -m "refactor(db): optimize user query performance"

# Performance improvement
git commit -m "perf(search): implement search result caching"

# Breaking change
git commit -m "feat!: change authentication API

BREAKING CHANGE: The authenticate() method now requires
an additional parameter for token expiration time."
```

### Message Guidelines

```bash
# Good commit messages:
git commit -m "Fix memory leak in user session handling"
git commit -m "Add email validation to registration form"
git commit -m "Update dependencies to resolve security vulnerabilities"

# Poor commit messages to avoid:
git commit -m "fix stuff"
git commit -m "changes"
git commit -m "WIP"
git commit -m "update"
```

## Interactive Commit Workflows

### Selective Commit from Staging

```bash
# Stage specific changes
git add -p complex-file.js

# Review what's staged
git diff --staged

# Commit staged changes
git commit -m "Refactor data processing logic"

# Continue with remaining changes
git diff  # See what's left unstaged
```

### Commit Template Usage

```bash
# Set up commit message template
git config --global commit.template ~/.gitmessage.txt

# Create template file
cat > ~/.gitmessage.txt << EOF
# <type>(<scope>): <subject>
#
# <body>
#
# <footer>

# Types: feat, fix, docs, style, refactor, perf, test, chore
# Scope: component or area of change
# Subject: imperative, present tense, no period, max 50 chars
# Body: motivation for change, wrap at 72 chars
# Footer: breaking changes, issue references
EOF

# Now git commit opens template
git commit
```

## Commit Verification

### Pre-commit Checks

```bash
# Commit with verbose output (shows diff in editor)
git commit -v

# Check what will be committed
git diff --staged

# Verify file status
git status

# Run tests before committing (manual)
npm test && git commit -m "Add new feature with tests"
```

### Post-commit Verification

```bash
# View the commit just made
git show HEAD

# Check commit details
git log -1 --stat

# Verify commit hash
git rev-parse HEAD
```

## Advanced Commit Scenarios

### Partial File Commits

```bash
# Stage parts of a file
git add -p large-file.js

# Commit staged portions
git commit -m "Implement core logic in large-file.js"

# File now has both committed and uncommitted changes
git status
# On branch main
# Changes to be committed:
#   (none)
# Changes not staged for commit:
#   modified: large-file.js
```

### Multiple Logical Changes

```bash
# Make multiple unrelated changes
# Edit feature1.js, feature2.js, bugfix.js

# Commit changes separately
git add feature1.js
git commit -m "feat: implement feature 1"

git add feature2.js
git commit -m "feat: implement feature 2"

git add bugfix.js
git commit -m "fix: resolve critical bug in data processing"
```

### Emergency Commits

```bash
# Quick commit for urgent fix
git add hotfix.js
git commit -m "hotfix: patch security vulnerability"

# Detailed follow-up commit
git add tests.js documentation.md
git commit -m "Add tests and docs for security hotfix

- Add comprehensive tests for security patch
- Update security documentation
- Add monitoring for similar vulnerabilities"
```

## Commit Hooks Integration

### Pre-commit Hook Example

```bash
#!/bin/sh
# .git/hooks/pre-commit

# Run tests
echo "Running tests..."
npm test
if [ $? -ne 0 ]; then
    echo "Tests failed. Commit aborted."
    exit 1
fi

# Check code formatting
echo "Checking code formatting..."
npm run lint
if [ $? -ne 0 ]; then
    echo "Linting failed. Commit aborted."
    exit 1
fi

echo "Pre-commit checks passed!"
exit 0
```

### Commit Message Hook

```bash
#!/bin/sh
# .git/hooks/commit-msg

commit_regex="^(feat|fix|docs|style|refactor|perf|test|chore)(\(.+\))?: .{1,50}$"

if ! grep -qE "$commit_regex" "$1"; then
    echo "Invalid commit message format!"
    echo "Format: type(scope): description"
    echo "Example: feat(auth): add login functionality"
    exit 1
fi
```

## Troubleshooting Commits

### Common Commit Problems

```bash
# Forgot to stage files
git status  # Shows unstaged changes
git add forgotten-file.txt
git commit --amend --no-edit

# Wrong commit message
git commit --amend -m "Corrected commit message"

# Committed to wrong branch
git log --oneline -1  # Note commit hash
git reset --hard HEAD~1  # Remove commit from current branch
git checkout correct-branch
git cherry-pick <commit-hash>  # Apply to correct branch
```

### Fixing Recent Commits

```bash
# Add files to last commit
git add missing-file.txt
git commit --amend --no-edit

# Change last commit message
git commit --amend -m "Better commit message"

# Change last commit author
git commit --amend --author="Correct Author <correct@email.com>"

# Completely redo last commit
git reset --soft HEAD~1  # Uncommit but keep changes staged
git commit -m "Completely new commit message"
```

### Large Commit Issues

```bash
# Commit is too large - split it
git reset --soft HEAD~1  # Undo commit, keep changes staged
git reset  # Unstage all changes

# Now stage and commit in smaller pieces
git add part1-files
git commit -m "Part 1: core functionality"

git add part2-files
git commit -m "Part 2: error handling"
```

## Commit Strategies

### Atomic Commits

```bash
# One logical change per commit
git add user-model.js
git commit -m "Add User model class"

git add user-controller.js
git commit -m "Add User controller with CRUD operations"

git add user-routes.js
git commit -m "Add User API routes"

git add user-tests.js
git commit -m "Add comprehensive User model tests"
```

### Feature Branch Commits

```bash
# On feature branch, commit frequently
git checkout -b feature/user-authentication

git add auth-service.js
git commit -m "Add basic authentication service"

git add password-hash.js
git commit -m "Implement password hashing utility"

git add login-endpoint.js
git commit -m "Add login API endpoint"

git add auth-middleware.js
git commit -m "Add authentication middleware"

# When feature is complete, consider squashing
git rebase -i main  # Interactive rebase to clean history
```

### Release Commits

```bash
# Prepare release commit
git add package.json CHANGELOG.md
git commit -m "Release version 2.1.0

- Add user authentication system
- Improve performance by 25%
- Fix critical security vulnerabilities
- Update all dependencies to latest versions

Breaking Changes:
- Authentication API now requires API key header"

# Tag the release
git tag -a v2.1.0 -m "Version 2.1.0"
```

## Related Commands

- [[git-add]] - Stage changes for commit
- [[git-status]] - Check what can be committed
- [[git-diff]] - Review changes before commit
- [[git-log]] - View commit history
- [[git-show]] - Display commit details

## Examples

```bash
# Basic workflow
git status                           # Check current state
git add src/auth.js                  # Stage specific file
git commit -m "Add authentication"   # Commit with message

# Interactive workflow
git add -p                           # Stage interactively
git commit -v                        # Commit with verbose diff

# Amend workflow
git add forgotten-file.js            # Stage forgotten file
git commit --amend --no-edit         # Add to last commit

# Multi-part feature
git add core-logic.js
git commit -m "feat(auth): implement core authentication logic"

git add error-handling.js
git commit -m "feat(auth): add comprehensive error handling"

git add tests.js
git commit -m "test(auth): add authentication test suite"
```
