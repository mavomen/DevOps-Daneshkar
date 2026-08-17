---
id: git-add
aliases: []
tags: []
---

# git add

Stage changes from the working directory to the staging area in preparation for committing.

## Syntax

```bash
git add [<pathspec>...]
git add [options] [<pathspec>...]
```

## Description

The `git add` command stages changes from your [[WorkingDirectory]] to the [[StagingArea]]. It tells Git which changes you want to include in your next [[Commit]]. Files must be staged before they can be committed.

## Basic Usage

### Stage Specific Files

```bash
# Stage single file
git add filename.txt

# Stage multiple files
git add file1.txt file2.js file3.css

# Stage file with spaces in name
git add "file with spaces.txt"
```

### Stage by Pattern

```bash
# Stage all JavaScript files
git add '*.js'

# Stage all files in directory
git add src/

# Stage all CSS files in subdirectories
git add '**/*.css'

# Stage files by extension
git add *.txt *.md
```

### Stage All Changes

```bash
# Stage all changes (new, modified, deleted)
git add .

# Stage all changes in entire repository
git add -A

# Stage only tracked files (no new files)
git add -u
```

## Interactive Staging

### Patch Mode (-p)

```bash
# Stage changes interactively
git add -p filename.txt

# Interactive options:
# y - stage this hunk
# n - do not stage this hunk
# q - quit; do not stage this hunk or any remaining ones
# a - stage this hunk and all later hunks in the file
# d - do not stage this hunk or any later hunks in the file
# s - split the current hunk into smaller hunks
# e - manually edit the current hunk
# ? - print help
```

### Interactive Mode (-i)

```bash
# Enter interactive staging mode
git add -i

# Interactive menu:
# 1: status        - show paths with changes
# 2: update        - add working tree state to index
# 3: revert        - revert staged changes to HEAD
# 4: add untracked - add untracked paths to index
# 5: patch         - pick hunks and update selectively
# 6: diff          - view diff between HEAD and index
# 7: quit          - exit interactive mode
```

## Advanced Options

### Force Add Ignored Files

```bash
# Add file even if it's in .gitignore
git add -f ignored-file.txt
git add --force ignored-file.txt

# Check what's being ignored
git add -f *.log
```

### Intent to Add

```bash
# Mark untracked file as "will be added"
git add -N newfile.txt
git add --intent-to-add newfile.txt

# Allows git diff to show new files
git diff newfile.txt
```

### Verbose Output

```bash
# Show what's being added
git add -v filename.txt
git add --verbose *.js
```

### Dry Run

```bash
# Show what would be added without actually adding
git add -n .
git add --dry-run src/
```

## File State Examples

### New File

```bash
# Create new file
echo "Hello World" > hello.txt

# Stage new file
git add hello.txt

# Check status
git status
# Changes to be committed:
#   new file: hello.txt
```

### Modified File

```bash
# Modify existing file
echo "Additional content" >> existing.txt

# Stage modification
git add existing.txt

# Check status
git status
# Changes to be committed:
#   modified: existing.txt
```

### Deleted File

```bash
# Delete file
rm unwanted.txt

# Stage deletion
git add unwanted.txt
# or
git rm unwanted.txt

# Check status
git status
# Changes to be committed:
#   deleted: unwanted.txt
```

### Renamed File

```bash
# Rename file using git
git mv oldname.txt newname.txt

# Status automatically shows rename
git status
# Changes to be committed:
#   renamed: oldname.txt -> newname.txt

# Manual rename (Git detects if similarity > 50%)
mv manual-old.txt manual-new.txt
git add manual-new.txt
git rm manual-old.txt
```

## Partial Staging Workflows

### Stage Parts of File

```bash
# Make multiple changes to file
echo "Change 1" >> file.txt
echo "Change 2" >> file.txt

# Stage selectively
git add -p file.txt
# Choose which changes to stage

# File now has both staged and unstaged changes
git status
# Changes to be committed:
#   modified: file.txt
# Changes not staged for commit:
#   modified: file.txt
```

### Split Large Changes

```bash
# After making large changes
git add -p large-file.js

# Use 's' option to split hunks
# Use 'e' option to manually edit hunks
# Stage logical pieces separately
```

## Common Patterns

### Web Development

```bash
# Stage HTML, CSS, and JavaScript
git add '*.html' '*.css' '*.js'

# Stage source files only
git add src/ docs/

# Exclude build files
git add . --exclude='dist/*'
```

### Source Code Organization

```bash
# Stage implementation files
git add src/ lib/

# Stage tests separately
git add test/ spec/

# Stage documentation
git add docs/ README.md *.md
```

### Selective Commit Workflow

```bash
# Make multiple changes
# Edit feature1.js, feature2.js, debug.js

# Stage feature commits separately
git add feature1.js
git commit -m "Implement feature 1"

git add feature2.js
git commit -m "Implement feature 2"

# Leave debug changes unstaged for now
git status  # debug.js still modified
```

## Staging Best Practices

### Review Before Adding

```bash
# Check what changed
git status
git diff

# Review specific file changes
git diff filename.txt

# Stage after review
git add filename.txt
```

### Stage Logically Related Changes

```bash
# Good: Related changes together
git add auth.js login.html auth.css
git commit -m "Implement user authentication"

# Better: Use interactive staging for complex files
git add -p complex-file.js
git commit -m "Refactor data processing logic"
```

### Incremental Staging

```bash
# For large features, stage incrementally
git add core-logic.js
git commit -m "Add core processing logic"

git add error-handling.js
git commit -m "Add error handling"

git add tests.js
git commit -m "Add unit tests"
```

## Troubleshooting

### File Not Being Added

```bash
# Check if file is ignored
git status --ignored
git check-ignore filename.txt

# Force add if ignored
git add -f filename.txt

# Check file exists
ls -la filename.txt
```

### Staging Area Confusion

```bash
# Show staged changes
git diff --staged

# Show unstaged changes
git diff

# Clear staging area
git restore --staged .

# Start over with selective staging
git add -p
```

### Large File Issues

```bash
# Git may warn about large files
git add large-file.bin
# Warning: adding a 100MB file

# Use Git LFS for large files
git lfs track "*.bin"
git add .gitattributes
git add large-file.bin
```

### Permission Issues

```bash
# Fix file permissions before adding
chmod 644 filename.txt
git add filename.txt

# Git tracks executable bit
chmod +x script.sh
git add script.sh
# Git will track as executable
```

## Advanced Use Cases

### Sparse Staging

```bash
# Stage files matching complex criteria
find . -name "*.js" -not -path "./node_modules/*" -exec git add {} +

# Stage modified files only (skip new files)
git diff --name-only | xargs git add

# Stage files modified in last hour
find . -newermt "1 hour ago" -name "*.txt" -exec git add {} +
```

### Scripted Staging

```bash
#!/bin/bash
# Stage all source files
git add src/ lib/ include/

# Stage documentation if it exists
[ -d "docs" ] && git add docs/
[ -f "README.md" ] && git add README.md

# Skip staging if no changes
if git diff --staged --quiet; then
    echo "No changes to stage"
    exit 0
fi

echo "Staged changes:"
git diff --staged --name-only
```

### Conditional Staging

```bash
# Stage only if tests pass
if npm test; then
    git add .
    echo "Tests passed, changes staged"
else
    echo "Tests failed, not staging changes"
fi
```

## Examples

```bash
# Basic staging workflow
git status                    # Check current state
git diff                      # Review changes
git add src/main.js          # Stage specific file
git diff --staged            # Review staged changes
git commit -m "Update logic" # Commit staged changes

# Interactive staging workflow
git add -p                   # Stage interactively
git status                   # Check what's staged
git commit -m "Partial fix"  # Commit staged portions
git diff                     # See remaining changes

# Bulk staging with patterns
git add '*.js' '*.css'       # Stage by file type
git add src/ test/           # Stage by directory
git add -A                   # Stage everything
```


## Related Notes

- [[git-status]] - Check what needs to be staged
- [[git-diff]] - See changes before staging
- [[git-commit]] - Commit staged changes
- [[git-restore]] - Unstage or discard changes
- [[git-rm]] - Stage file deletions
