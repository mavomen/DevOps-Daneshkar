---
id: git-show
aliases: []
tags: []
---

# git show

Display detailed information about Git objects, including commits, trees, blobs, and tags.

## Syntax

```bash
git show [<options>] [<object>...]
```

## Description

The `git show` command displays the content and metadata of Git objects. Most commonly used to show detailed information about [[Commit]]s, including the commit message, author information, timestamp, and the actual changes (diff) introduced by that commit.

## Basic Usage

### Show Specific Commit

```bash
# Show the most recent commit
git show

# Show specific commit by hash
git show 1a2b3c4

# Show commit by relative reference
git show HEAD~1
git show HEAD^

# Show commit by branch name (shows tip of branch)
git show main
git show feature-branch
```

### Show Tags

```bash
# Show tag information
git show v1.0.0

# Show annotated tag details
git show --name-only v1.0.0

# Show tag and associated commit
git show v1.0.0^{commit}
```

### Show Trees and Blobs

```bash
# Show tree object (directory structure)
git show HEAD:src/

# Show specific file content from commit
git show HEAD:src/app.js
git show 1a2b3c4:README.md

# Show file from different branch
git show feature-branch:src/newfile.js
```

## Output Formats

### Default Output

```bash
git show 1a2b3c4

# Example output:
# commit 1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b
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
# diff --git a/src/auth.js b/src/auth.js
# new file mode 100644
# index 0000000..1a2b3c4
# --- /dev/null
# +++ b/src/auth.js
# @@ -0,0 +1,25 @@
# +const bcrypt = require('bcrypt');
# +const jwt = require('jsonwebtoken');
# +
# +function hashPassword(password) {
# +  return bcrypt.hash(password, 10);
# +}
# ...
```

### Statistics Only

```bash
# Show commit info and file statistics
git show --stat

# Example output:
# commit 1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b
# Author: John Doe <john@example.com>
# Date:   Mon Jan 15 10:30:45 2024 -0700
#
#     Add user authentication system
#
#  src/auth.js       | 25 +++++++++++++++++++++++++
#  src/middleware.js | 15 +++++++++++++++
#  package.json      |  3 +++
#  3 files changed, 43 insertions(+)

# Show short statistics
git show --shortstat

# Show only number statistics
git show --numstat
```

### Name Only

```bash
# Show only changed file names
git show --name-only

# Show changed files with status
git show --name-status

# Example output:
# commit 1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b
# Author: John Doe <john@example.com>
# Date:   Mon Jan 15 10:30:45 2024 -0700
#
#     Add user authentication system
#
# A       src/auth.js
# M       src/middleware.js
# M       package.json
```

## Formatting Options

### Pretty Formats

```bash
# Use predefined formats
git show --pretty=oneline
git show --pretty=short
git show --pretty=full
git show --pretty=fuller

# Custom format
git show --pretty=format:"%h - %an, %ar : %s"
git show --pretty=format:"%C(yellow)%h%C(reset) %C(blue)%ad%C(reset) %s" --date=short
```

### No Patch Output

```bash
# Show commit info without diff
git show --no-patch 1a2b3c4
git show -s 1a2b3c4  # -s is shorthand for --no-patch

# Show multiple commits without diffs
git show --no-patch HEAD~3 HEAD~2 HEAD~1 HEAD
```

### Custom Diff Options

```bash
# Show word-level differences
git show --word-diff

# Ignore whitespace changes
git show -w
git show --ignore-all-space

# Show context lines
git show -U10  # Show 10 lines of context
git show --unified=10

# Show function names in diff headers
git show -p --show-function-line
```

## Multiple Objects

### Show Multiple Commits

```bash
# Show several commits
git show HEAD~2 HEAD~1 HEAD

# Show range of commits
git show HEAD~3..HEAD

# Show commits with specific format
git show --pretty=oneline HEAD~3..HEAD
```

### Show Different Object Types

```bash
# Show commit, its tree, and a specific file
git show HEAD HEAD^{tree} HEAD:README.md

# Show tag and the commit it points to
git show v1.0.0 v1.0.0^{commit}
```

## File-Specific Views

### Show File at Specific Commit

```bash
# Show file content from specific commit
git show 1a2b3c4:src/app.js

# Show file from HEAD
git show HEAD:package.json

# Show file from different branch
git show feature-branch:src/newfile.js

# Show file that no longer exists
git show HEAD~5:deleted-file.txt
```

### Show Directory Structure

```bash
# Show directory tree from commit
git show HEAD:src/

# Show root directory structure
git show HEAD:

# Show subdirectory from specific commit
git show 1a2b3c4:docs/api/
```

## Practical Workflows

### Code Review

```bash
# Review specific commit
git show 1a2b3c4

# Review with context
git show -U5 1a2b3c4

# Review multiple commits
git show HEAD~3..HEAD --stat

# Review without merge commits
git show --no-merges HEAD~10..HEAD
```

### Debugging and Investigation

```bash
# Check what changed in problematic commit
git show --stat suspicious-commit

# See exact changes in specific file
git show problematic-commit -- src/buggy-file.js

# Compare file versions
git show HEAD:file.txt
git show HEAD~5:file.txt
```

### Release and Documentation

```bash
# Show changes in release commit
git show v2.1.0 --stat

# Document specific implementation
git show implementation-commit:src/feature.js

# Show configuration changes
git show config-commit:config/settings.json
```

### File History Exploration

```bash
# Show file at different points in time
git show HEAD:README.md        # Current version
git show HEAD~1:README.md      # Previous version
git show HEAD~10:README.md     # Much earlier version

# Show deleted file from when it existed
git show HEAD~20:old-feature.js
```

## Advanced Usage

### Object Inspection

```bash
# Show object type and size
git show --format=raw 1a2b3c4

# Show commit object details
git show --pretty=fuller 1a2b3c4

# Show signature information (if commit is signed)
git show --show-signature 1a2b3c4
```

### Binary Files

```bash
# Show changes in binary files
git show --binary 1a2b3c4

# Show summary for binary files
git show --stat 1a2b3c4

# Force text view of binary file
git show --text 1a2b3c4:binary-file.dat
```

### Merge Commits

```bash
# Show merge commit
git show merge-commit

# Show changes introduced by merge (not just merge commit)
git show --first-parent merge-commit

# Show what was merged
git show merge-commit^2

# Compare merge parents
git show merge-commit^1 merge-commit^2
```

## Output Control

### Paging and Color

```bash
# Disable pager
git --no-pager show 1a2b3c4

# Force color output (useful for pipes)
git show --color=always 1a2b3c4

# No color output
git show --color=never 1a2b3c4
```

### Limiting Output

```bash
# Show only first few lines of diff
git show 1a2b3c4 | head -50

# Show without diff context
git show --no-patch 1a2b3c4

# Show with minimal context
git show -U0 1a2b3c4
```

## Integration with Other Tools

### Piping to Other Commands

```bash
# Search in commit changes
git show 1a2b3c4 | grep "function"

# Save commit details to file
git show 1a2b3c4 > commit-details.txt

# Count lines changed
git show --numstat 1a2b3c4 | awk '{sum += $1 + $2} END {print sum}'

# Extract just the commit message
git show --pretty=format:"%B" --no-patch 1a2b3c4
```

### Scripting with git show

```bash
#!/bin/bash
# Show summary of recent commits

for commit in $(git rev-list --max-count=5 HEAD); do
    echo "=== Commit $commit ==="
    git show --pretty=format:"%h %an %ar: %s" --stat $commit
    echo
done
```

## Troubleshooting

### Common Issues

```bash
# Object not found
git show nonexistent-commit
# fatal: bad object nonexistent-commit

# Ambiguous reference
git show 1a2  # If multiple objects start with 1a2
# Use more characters or full hash

# Large output handling
git show large-commit | less  # Use pager
git show --stat large-commit  # Show summary only
```

### Performance Considerations

```bash
# For large commits, show summary first
git show --stat 1a2b3c4

# Skip large binary files
git show --text=false 1a2b3c4

# Show specific files only
git show 1a2b3c4 -- src/specific-file.js
```

## Examples

```bash
# Basic commit inspection
git show                              # Show latest commit
git show HEAD~1                       # Show previous commit
git show 1a2b3c4                     # Show specific commit

# File content at different times
git show HEAD:README.md               # Current version
git show v1.0.0:README.md            # Version from tag
git show feature-branch:src/app.js   # From different branch

# Statistical views
git show --stat HEAD                  # Commit with file statistics
git show --name-only HEAD             # Just show changed files
git show --shortstat HEAD             # Brief statistics

# Formatted output
git show --pretty=oneline HEAD        # One-line format
git show --no-patch HEAD              # No diff, just metadata
git show --word-diff HEAD             # Word-level differences

# Multiple objects
git show HEAD~3 HEAD~2 HEAD~1        # Show multiple commits
git show v1.0.0 v2.0.0               # Show multiple tags
```


## Related Notes

- [[git-log]] - Show commit history
- [[git-diff]] - Compare versions
- [[git-cat-file]] - Show raw object content
- [[git-ls-tree]] - List tree objects
- [[git-blame]] - Show line-by-line attribution
