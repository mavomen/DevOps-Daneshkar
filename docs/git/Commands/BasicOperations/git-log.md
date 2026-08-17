---
id: git-log
aliases: []
tags: []
---

# git log

Display the commit history of a repository, showing commits with their messages, authors, dates, and other metadata.

## Syntax

```bash
git log [<options>] [<revision-range>] [[--] <path>...]
```

## Description

The `git log` command shows the [[GitHistory]] by displaying commits in reverse chronological order (newest first). It's the primary tool for exploring what happened in your project over time and understanding the evolution of your codebase.

## Basic Usage

### Standard Log Output

```bash
# Show commit history
git log

# Example output:
# commit 1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b (HEAD -> main, origin/main)
# Author: John Doe <john@example.com>
# Date:   Mon Jan 15 10:30:45 2024 -0700
#
#     Add user authentication system
#
#     - Implement JWT token authentication
#     - Add password hashing with bcrypt
#     - Create authentication middleware
#     - Add user session management
#
# commit 5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c3d4e
# Author: Jane Smith <jane@example.com>
# Date:   Sun Jan 14 14:22:15 2024 -0700
#
#     Fix navigation menu styling
```

### Concise Log Formats

```bash
# One line per commit
git log --oneline

# Example output:
# 1a2b3c4 (HEAD -> main, origin/main) Add user authentication system
# 5d6e7f8 Fix navigation menu styling
# 9a8b7c6 Update dependencies to latest versions
# 2c3d4e5 Initial project setup

# Short format with abbreviated info
git log --pretty=short

# Medium format (default)
git log --pretty=medium
```

### Limiting Output

```bash
# Show only last 5 commits
git log -5
git log -n 5

# Show commits from last week
git log --since="1 week ago"

# Show commits from specific date range
git log --since="2024-01-01" --until="2024-01-31"

# Show commits by specific author
git log --author="John Doe"
```

## Advanced Formatting

### Custom Format Strings

```bash
# Custom format
git log --pretty=format:"%h - %an, %ar : %s"
# Output: 1a2b3c4 - John Doe, 2 days ago : Add authentication

# Detailed custom format
git log --pretty=format:"%C(yellow)%h%C(reset) %C(blue)%ad%C(reset) %C(green)%an%C(reset) %s" --date=short

# Common format placeholders:
# %H  - Full commit hash
# %h  - Abbreviated commit hash
# %an - Author name
# %ae - Author email
# %ad - Author date
# %ar - Author date, relative
# %cn - Committer name
# %cd - Committer date
# %s  - Commit subject (first line of message)
# %b  - Commit body
# %d  - Ref names (branches, tags)
```

### Predefined Formats

```bash
# Full format (shows everything)
git log --pretty=full

# Fuller format (includes committer info)
git log --pretty=fuller

# Email patch format
git log --pretty=email

# Raw format (shows raw commit object)
git log --pretty=raw
```

### Graphical Output

```bash
# Show branch and merge history as ASCII graph
git log --graph

# Combine with oneline for clean view
git log --graph --oneline

# All branches and tags
git log --graph --oneline --all

# Decorate with branch/tag names
git log --graph --oneline --decorate --all

# Create alias for common graph view
git config --global alias.lg "log --graph --oneline --decorate --all"
```

## Filtering and Searching

### By Author and Committer

```bash
# Commits by specific author
git log --author="John Doe"

# Multiple authors (regex pattern)
git log --author="John\|Jane"

# Commits by committer
git log --committer="build-bot"

# Author email domain
git log --author="@company.com"
```

### By Date and Time

```bash
# Commits since specific date
git log --since="2024-01-15"
git log --after="2024-01-15"

# Commits until specific date
git log --until="2024-01-20"
git log --before="2024-01-20"

# Relative date ranges
git log --since="2 weeks ago"
git log --since="3 days ago"
git log --until="yesterday"

# Specific time range
git log --since="2024-01-15 10:00" --until="2024-01-15 18:00"
```

### By Commit Message

```bash
# Search commit messages (case-insensitive)
git log --grep="bug fix"

# Case-sensitive search
git log --grep="Bug Fix"

# Multiple patterns (OR)
git log --grep="bug" --grep="fix"

# Multiple patterns (AND)
git log --grep="bug" --grep="fix" --all-match

# Invert match (exclude commits with pattern)
git log --grep="WIP" --invert-grep
```

### By File Changes

```bash
# Commits that modified specific file
git log -- filename.txt

# Commits that modified files in directory
git log -- src/

# Commits that modified any JavaScript file
git log -- '*.js'

# Follow file through renames
git log --follow -- oldname.txt

# Commits that added or removed specific string
git log -S "function_name"

# Commits that added or removed lines matching regex
git log -G "regex_pattern"
```

## Commit Range Specifications

### Range Syntax

```bash
# Commits between two points
git log commit1..commit2

# Commits reachable from commit2 but not from commit1
git log commit1..commit2

# Commits reachable from either commit1 or commit2
git log commit1...commit2

# All commits since branch point (symmetric difference)
git log main...feature-branch
```

### Branch Comparisons

```bash
# Commits in feature branch not in main
git log main..feature-branch

# Commits in main not in feature branch
git log feature-branch..main

# Show commits unique to each branch
git log --left-right main...feature-branch

# Commits since common ancestor
git log $(git merge-base main feature-branch)..feature-branch
```

### Reference Specifications

```bash
# Commits from HEAD to 3 commits back
git log HEAD~3..HEAD

# Last 5 commits on current branch
git log -5

# Commits on current branch not on main
git log main..HEAD

# All commits reachable from any reference
git log --all
```

## File and Directory Specific

### Path-Limited Logs

```bash
# History of specific file
git log -- path/to/file.txt

# History of directory
git log -- src/

# Multiple paths
git log -- src/ docs/ README.md

# Exclude paths
git log -- . ':(exclude)*.log' ':(exclude)node_modules'
```

### File Content Changes

```bash
# Show patches (actual changes) with log
git log -p

# Show patches for specific file
git log -p -- filename.txt

# Show only patches that change specific content
git log -S "search_string" -p

# Show statistics with each commit
git log --stat

# Show short statistics
git log --shortstat
```

### Follow File History

```bash
# Follow file through renames and moves
git log --follow -- file.txt

# Show patches following renames
git log --follow -p -- file.txt

# Find when file was deleted
git log --diff-filter=D --summary

# Find when file was added
git log --diff-filter=A --name-status
```

## Specialized Log Views

### Merge Commits

```bash
# Show only merge commits
git log --merges

# Exclude merge commits
git log --no-merges

# Show merge commits with first parent only
git log --first-parent

# Show what commits were merged
git log --merges --pretty=format:"%h %s" --graph
```

### Tag and Release Information

```bash
# Commits since last tag
git log $(git describe --tags --abbrev=0)..HEAD

# Commits between two tags
git log v1.0.0..v2.0.0

# Show tags in log
git log --decorate

# Find commits that introduced tags
git log --simplify-by-decoration
```

### Statistical Views

```bash
# Contribution statistics by author
git log --pretty=format:"%an" | sort | uniq -c | sort -rn

# Shortlog summary by author
git shortlog

# Shortlog with commit counts
git shortlog -sn

# Lines changed by author
git log --author="John Doe" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }'
```

## Performance and Large Repositories

### Limiting for Performance

```bash
# Limit to recent commits
git log --since="1 month ago"

# Limit output size
git log -n 100

# Simplify history for performance
git log --simplify-merges

# Skip merge commits for cleaner history
git log --no-merges

# First parent only (linear history view)
git log --first-parent
```

### Sparse Checkout Friendly

```bash
# Only show commits affecting current sparse checkout
git log --sparse

# Show commits that affect currently checked out files
git log --dense
```

## Output Control

### Paging and Formatting

```bash
# Disable pager (output all at once)
git --no-pager log

# Use specific pager
git config core.pager "less -R"

# Force color output
git log --color=always

# Disable color output
git log --color=never
```

### Machine Readable Output

```bash
# Porcelain format for scripts
git log --pretty=format:"%H|%an|%ad|%s" --date=iso

# JSON-like format (requires git 2.1+)
git log --pretty=format:'{"hash":"%H","author":"%an","date":"%ad","message":"%s"}' --date=iso

# Export as patches
git log --pretty=email --patch
```

## Practical Workflows

### Code Review Preparation

```bash
# Review all commits in feature branch
git log main..feature-branch --oneline

# See detailed changes
git log main..feature-branch -p

# Get overview of changes
git log main..feature-branch --stat

# Check for fixup commits that should be squashed
git log main..feature-branch --oneline | grep "fixup\|squash"
```

### Release Notes Generation

```bash
# Changes since last release
git log v1.2.0..HEAD --oneline

# Group by type (requires conventional commits)
git log v1.2.0..HEAD --oneline | grep "^feat:"
git log v1.2.0..HEAD --oneline | grep "^fix:"

# Get detailed release notes
git log v1.2.0..HEAD --pretty=format:"- %s (%an)" --no-merges
```

### Debugging and Investigation

```bash
# Find when bug was introduced
git log --since="2 weeks ago" --grep="auth" -p

# See who worked on specific area
git log --author="" --since="1 month ago" -- src/auth/

# Find specific commit by partial hash
git log --grep="1a2b3c"

# Search for commits that mention issue number
git log --grep="#123"
```

### Team Coordination

```bash
# See team activity
git log --since="1 week ago" --pretty=format:"%an: %s" --no-merges

# Find commits by multiple team members
git log --author="John\|Jane\|Bob" --since="1 month ago" --oneline

# See merge activity
git log --merges --pretty=format:"%h %s (%an)" --since="1 week ago"
```

## Examples

```bash
# Basic log usage
git log                               # Full commit history
git log --oneline                     # Condensed one-line format
git log -5                           # Last 5 commits
git log --since="1 week ago"         # Recent commits

# Visual and formatted logs
git log --graph --oneline --all       # ASCII graph of all branches
git log --pretty=format:"%h %s (%an)" # Custom format
git log --stat                        # With file change statistics

# Filtering and searching
git log --author="John Doe"           # Commits by specific author
git log --grep="bug fix"              # Search commit messages
git log -- src/auth.js               # History of specific file
git log main..feature                 # Commits in feature not in main

# Analysis and investigation
git shortlog -sn                      # Author contribution summary
git log -S "function_name" -p         # Find changes to specific code
git log --follow -- renamed-file.txt  # Follow file through renames
```


## Related Notes

- [[git-show]] - Display specific commits
- [[git-blame]] - Show who changed each line
- [[git-reflog]] - Show reference history
- [[git-shortlog]] - Summarized log by author
- [[GitHistory]] - Understanding repository history
