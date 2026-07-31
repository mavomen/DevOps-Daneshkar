---
id: git-diff
aliases: []
tags: []
---

# git diff

Show changes between different versions of files, commits, branches, or between the working directory and staging area.

## Syntax

```bash
git diff [<options>] [<commit>] [--] [<path>...]
git diff [<options>] <commit>..<commit> [--] [<path>...]
git diff [<options>] <commit>...<commit> [--] [<path>...]
```

## Description

The `git diff` command shows differences between various states of your repository. It can compare the [[WorkingDirectory]] with the [[StagingArea]], compare commits, branches, or show what changed in specific files over time.

## Basic Usage

### Working Directory Comparisons

```bash
# Show unstaged changes (working directory vs staging area)
git diff

# Show staged changes (staging area vs last commit)
git diff --staged
git diff --cached  # Same as --staged

# Show all changes (working directory vs last commit)
git diff HEAD

# Compare working directory with specific commit
git diff HEAD~2
git diff 1a2b3c4
```

### File-Specific Diffs

```bash
# Show changes in specific file
git diff filename.txt

# Show staged changes in specific file
git diff --staged filename.txt

# Show changes in specific file vs specific commit
git diff HEAD~1 filename.txt
```

### Directory-Specific Diffs

```bash
# Show changes in specific directory
git diff src/

# Show changes in multiple directories
git diff src/ docs/

# Show changes with path filtering
git diff '*.js'
```

## Commit Comparisons

### Compare Commits

```bash
# Compare two commits
git diff 1a2b3c4 5d6e7f8

# Compare commit with its parent
git diff 1a2b3c4^ 1a2b3c4
git diff 1a2b3c4~1 1a2b3c4

# Compare with previous commits
git diff HEAD~1      # Compare with previous commit
git diff HEAD~2      # Compare with 2 commits ago
git diff HEAD~1..HEAD  # Explicit range syntax
```

### Branch Comparisons

```bash
# Compare current branch with another branch
git diff main
git diff origin/main

# Compare two branches
git diff main feature-branch

# Compare branches at specific points
git diff main...feature-branch  # Show changes in feature-branch since common ancestor
```

### Tag Comparisons

```bash
# Compare with tagged version
git diff v1.0.0

# Compare two tags
git diff v1.0.0 v2.0.0

# Compare current state with tag
git diff HEAD v1.0.0
```

## Output Formats

### Default Output

```bash
git diff filename.txt

# Example output:
# diff --git a/filename.txt b/filename.txt
# index 1a2b3c4..5d6e7f8 100644
# --- a/filename.txt
# +++ b/filename.txt
# @@ -1,4 +1,6 @@
#  line 1
#  line 2
# -old line 3
# +new line 3
# +added line 4
#  line 4
```

### Alternative Formats

```bash
# Word-level diff instead of line-level
git diff --word-diff

# Color-coded word diff
git diff --word-diff=color

# Character-level diff
git diff --word-diff-regex=.

# Side-by-side comparison
git diff --no-index --word-diff=color file1.txt file2.txt
```

### Statistical Output

```bash
# Show only statistics
git diff --stat

# Example output:
#  src/app.js     | 15 +++++++--------
#  src/auth.js    | 23 +++++++++++++++++++++++
#  README.md      |  8 ++------
#  3 files changed, 32 insertions(+), 14 deletions(-)

# Show short statistics
git diff --shortstat

# Show number statistics
git diff --numstat
```

### Name-Only Output

```bash
# Show only changed file names
git diff --name-only

# Show changed files with status
git diff --name-status

# Example output:
# M       src/app.js
# A       src/auth.js
# D       old-file.txt
```

## Advanced Options

### Context Control

```bash
# Show more context lines (default is 3)
git diff -U5 filename.txt
git diff --unified=5 filename.txt

# Show entire file context
git diff --no-prefix -U1000 filename.txt

# Minimal context
git diff -U1 filename.txt
```

### Ignore Options

```bash
# Ignore whitespace differences
git diff -w
git diff --ignore-all-space

# Ignore whitespace at end of lines
git diff --ignore-space-at-eol

# Ignore changes in amount of whitespace
git diff -b
git diff --ignore-space-change

# Ignore blank lines
git diff --ignore-blank-lines
```

### File Filtering

```bash
# Diff only specific file types
git diff '*.js'
git diff '*.css' '*.html'

# Exclude specific files
git diff -- . ':(exclude)*.log'
git diff -- . ':(exclude)node_modules'

# Include only specific directories
git diff -- src/ docs/
```

### Movement Detection

```bash
# Detect file renames and moves
git diff -M
git diff --find-renames

# Set rename similarity threshold (default 50%)
git diff -M90%

# Detect copies in addition to renames
git diff -C
git diff --find-copies

# Detect copies from all files, not just modified ones
git diff --find-copies-harder
```

## Diff Tools Integration

### Configure External Diff Tool

```bash
# Set up external diff tool
git config --global diff.tool vimdiff
git config --global diff.tool meld
git config --global diff.tool kdiff3

# Configure custom diff tool
git config --global diff.tool vscode
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'

# Use external tool
git difftool
git difftool --staged
git difftool HEAD~1
```

### VS Code Integration

```bash
# Configure VS Code as diff tool
git config --global diff.tool vscode
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'
git config --global difftool.prompt false

# Use VS Code for diffs
git difftool filename.txt
git difftool --staged
```

## Practical Workflows

### Pre-Commit Review

```bash
# Review all changes before committing
git diff                    # See unstaged changes
git add -p                  # Stage selectively
git diff --staged           # Review staged changes
git commit -m "Add feature" # Commit after review
```

### Code Review Workflow

```bash
# Compare feature branch with main
git diff main...feature-branch

# See what files changed
git diff --name-only main...feature-branch

# Review specific commits
git diff HEAD~3..HEAD

# Compare with remote branch
git diff origin/main
```

### Bug Investigation

```bash
# See what changed since last release
git diff v1.2.0..HEAD

# Check specific file history
git diff HEAD~5..HEAD -- problematic-file.js

# Compare with known good state
git diff good-commit bad-commit -- src/
```

### Release Preparation

```bash
# See all changes since last tag
git diff v1.0.0..HEAD --stat

# Review changes by file type
git diff v1.0.0..HEAD '*.js' --stat
git diff v1.0.0..HEAD '*.md' --stat

# Get change summary
git diff v1.0.0..HEAD --shortstat
```

## Diff Output Understanding

### Reading Diff Headers

```bash
# diff --git a/file.txt b/file.txt
# index 1a2b3c4..5d6e7f8 100644
# --- a/file.txt     # Original file
# +++ b/file.txt     # Modified file
# @@ -1,4 +1,6 @@   # Hunk header: old range, new range
#  unchanged line    # Context line
# -removed line      # Deleted line
# +added line        # Added line
```

### Hunk Headers

```bash
# @@ -start,count +start,count @@
# @@ -1,4 +1,6 @@
# - Original file: starting at line 1, showing 4 lines
# + Modified file: starting at line 1, showing 6 lines
```

### Binary Files

```bash
git diff binary-file.png
# Binary files a/binary-file.png and b/binary-file.png differ

# Force text treatment of binary files
git diff --text binary-file.bin
```

## Performance and Large Files

### Handling Large Diffs

```bash
# Limit diff output
git diff | head -100

# Use pager for large diffs
git diff | less

# Skip large files
git diff --skip-large-files

# Set diff timeout
git config diff.timeout 10
```

### Repository-Specific Configuration

```bash
# Configure diff behavior per repository
git config diff.tool vimdiff
git config diff.algorithm patience
git config diff.renames true
```

## Troubleshooting

### Common Issues

```bash
# Diff shows no changes but files are modified
git status                    # Check file status
git diff --check             # Check for whitespace issues
git config core.autocrlf     # Check line ending settings

# Diff output is too verbose
git diff --stat              # Show summary only
git diff --name-only         # Show changed files only

# Can't see differences in binary files
file suspicious-file.txt     # Check if file is really text
git diff --text suspicious-file.txt  # Force text diff
```

### No Output Issues

```bash
# If git diff shows nothing:
git status                   # Check if changes are staged
git diff --staged            # Check staged changes
git diff HEAD                # Compare with last commit
```

### Encoding Issues

```bash
# Handle encoding problems
git config core.quotepath false
git diff --no-color | cat
git diff | iconv -f utf-8 -t ascii//TRANSLIT
```

## Advanced Use Cases

### Custom Diff Drivers

```bash
# Configure custom diff for specific file types
echo "*.json diff=json" >> .gitattributes
git config diff.json.textconv 'python -m json.tool'

# Now JSON files will be formatted before diffing
git diff config.json
```

### Ignoring Specific Changes

```bash
# Create clean script for comparison
git diff --ignore-all-space --ignore-blank-lines

# Use filters to ignore generated content
git diff -- . ':(exclude)package-lock.json'
git diff -- . ':(exclude)*.generated.js'
```

### Combining with Other Commands

```bash
# Pipe diff to other tools
git diff | grep "function"
git diff --name-only | xargs grep "TODO"

# Save diff to file
git diff > changes.patch
git apply changes.patch  # Apply patch later
```

## Related Commands

- [[git-status]] - See which files have changes
- [[git-add]] - Stage changes shown in diff
- [[git-show]] - Show changes in specific commit
- [[git-log]] - View commit history
- [[git-apply]] - Apply patch files

## Examples

```bash
# Basic diff commands
git diff                      # Unstaged changes
git diff --staged             # Staged changes
git diff HEAD                 # All changes since last commit

# Specific file/directory diffs
git diff src/app.js           # Changes in specific file
git diff src/                 # Changes in directory

# Commit comparisons
git diff HEAD~1               # Changes since previous commit
git diff main feature         # Differences between branches
git diff v1.0.0..HEAD         # Changes since version 1.0.0

# Formatted output
git diff --stat               # Statistics only
git diff --name-only          # File names only
git diff --word-diff          # Word-level differences
```
