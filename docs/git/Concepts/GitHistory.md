---
id: GitHistory
aliases: []
tags: []
---

# Git History

Git history is the complete record of all changes made to your project over time, stored as a chain of commits that preserves the evolution of your codebase.

## What is Git History?

Git history represents:

- Chronological sequence of all [[Commit]]s
- Complete project evolution timeline
- Relationships between different development paths
- Metadata about who changed what and when
- Foundation for collaboration and recovery

## History Structure

### Linear History

```mermaid
graph LR
    A[Initial Commit] --> B[Add Feature] --> C[Fix Bug] --> D[Release v1.0]
```

Simple, sequential development without branches.

### Branched History

```mermaid
graph LR
    A[Initial] --> B[Main Work]
    B --> C[More Main]
    B --> D[Feature Work]
    D --> E[Feature Complete]
    C --> F[Merge Feature]
    E --> F
```

Parallel development with feature branches.

### Complex History

```mermaid
graph TD
    A[main] --> B[develop]
    B --> C[feature/auth]
    B --> D[feature/ui]
    C --> E[Merge auth]
    D --> F[Merge ui]
    E --> B
    F --> B
    B --> G[release/v1.0]
    G --> H[main]
```

Multiple branches, merges, and releases.

## History Navigation

### Basic History Viewing

```bash
# View commit history
git log

# Concise history
git log --oneline

# Last 10 commits
git log -10

# Graphical history
git log --graph --oneline --all

# History with file changes
git log --stat
```

### History Filtering

```bash
# Commits by author
git log --author="John Doe"

# Commits in date range
git log --since="2024-01-01" --until="2024-02-01"

# Commits affecting specific file
git log -- path/to/file.js

# Commits with specific message
git log --grep="bug fix"

# Commits changing specific content
git log -S "function_name"
```

### History Formatting

```bash
# Custom format
git log --pretty=format:"%h - %an, %ar : %s"

# Show merge commits only
git log --merges

# Show non-merge commits only
git log --no-merges

# Show first-parent only (simplified)
git log --first-parent
```

## History Analysis

### Finding Changes

```bash
# What changed in specific commit
git show 1a2b3c4

# Files changed in commit
git show --name-only 1a2b3c4

# Line-by-line changes
git show 1a2b3c4 -- path/to/file.js

# Compare commits
git diff 1a2b3c4..5d6e7f8

# See commit that introduced line
git blame path/to/file.js
```

### Following File History

```bash
# Track file through renames
git log --follow -- path/to/file.js

# See when file was deleted
git log --diff-filter=D --summary

# See when files were added
git log --diff-filter=A --name-status

# History of specific function
git log -L :function_name:path/to/file.js
```

### Finding Problematic Changes

```bash
# Binary search for bugs
git bisect start
git bisect bad HEAD
git bisect good v1.0.0

# Find when bug was introduced
git log --grep="introduce.*bug"

# Track down performance regression
git log --since="1 month ago" --grep="performance"
```

## History Types

### Commit History

- Sequential record of commits
- Author and timestamp information
- Commit messages and descriptions
- Parent-child relationships

### File History

- Changes to specific files over time
- Renames and moves tracked
- Content evolution visible
- Blame information available

### Branch History

- Development path tracking
- Merge and split points
- Feature development lifecycle
- Integration patterns

### Tag History

- Release and milestone markers
- Version progression
- Important state snapshots
- Deployment references

## Working with History

### History Exploration

```bash
# Interactive history browsing
gitk --all &           # Graphical browser
git log --oneline --graph --all

# Recent activity
git log --since="1 week ago"

# Activity by team member
git shortlog -sn

# Most active files
git log --pretty=format: --name-only | sort | uniq -c | sort -rg | head -10
```

### History Searching

```bash
# Find commits by content
git log -S "important_function"

# Find commits by message
git log --grep="security"

# Find merge commits
git log --merges --oneline

# Find commits by file path
git log -- '*.js' --oneline

# Find commits between tags
git log v1.0.0..v2.0.0 --oneline
```

### History Statistics

```bash
# Commit count by author
git shortlog -sn

# Lines added/removed by author
git log --author="John" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }'

# Files changed most often
git log --pretty=format: --name-only | sort | uniq -c | sort -rg | head -10

# Commit activity over time
git log --pretty=format:"%ad" --date=short | uniq -c
```

## Related Notes

- [[GitHistoryManagement]] — Extended coverage
