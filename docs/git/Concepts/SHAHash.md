---
id: SHAHash
aliases: []
tags: []
---

# SHA Hash

A SHA (Secure Hash Algorithm) hash is Git's unique identifier for every object in the repository, including commits, trees, blobs, and tags.

## What is a SHA Hash?

A SHA hash is:

- A 40-character hexadecimal string
- Unique identifier for Git objects
- Cryptographically secure fingerprint
- Calculated from object content
- Immutable once created

## SHA Hash Format

### Full SHA Hash

```
1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b
```

- 40 hexadecimal characters (0-9, a-f)
- Also called "SHA-1" or "object ID"
- Uniquely identifies one specific object

### Abbreviated SHA Hash

```
1a2b3c4    # 7 characters (common)
1a2b3c4d   # 8 characters
1a2b3c4d5e # 10 characters
```

- Git uses shortest unambiguous abbreviation
- Usually 7 characters are sufficient
- Automatically expands to full hash when needed

## How SHA Hashes Work

### Hash Calculation

SHA hashes are calculated from:

- Object type (commit, tree, blob, tag)
- Object size
- Object content
- For commits: tree hash, parent hash(es), author, timestamp, message

### Content Addressable Storage

```bash
# Same content always produces same hash
echo "Hello World" | git hash-object --stdin
# Output: 557db03de997c86a4a028e1ebd3a1ceb225be238

# Different content produces different hash
echo "Hello World!" | git hash-object --stdin
# Output: 980a0d5f19a64b4b30a87d4206aade58726b60e3
```

## Using SHA Hashes

### Referencing Commits

```bash
# Full hash
git show 1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b

# Abbreviated hash (Git finds full match)
git show 1a2b3c4

# Minimum characters needed (varies by repo)
git show 1a2b
```

### Finding SHA Hashes

```bash
# Current commit hash
git rev-parse HEAD

# Branch tip hash
git rev-parse main

# Previous commit hash
git rev-parse HEAD~1

# Tag hash
git rev-parse v1.0.0

# Show all commit hashes
git log --oneline
```

## SHA Hash in Git Commands

### Checkout and Navigation

```bash
# Checkout specific commit
git checkout 1a2b3c4

# Create branch from specific commit
git branch hotfix 1a2b3c4d

# Reset to specific commit
git reset --hard 1a2b3c4
```

### Comparison and Differences

```bash
# Compare commits by hash
git diff 1a2b3c4..5d6e7f8

# Show changes in specific commit
git show 1a2b3c4

# List files changed in commit
git diff-tree --name-only 1a2b3c4
```

### History and Logging

```bash
# Show commit history with hashes
git log --oneline

# Search by commit hash
git log --grep="1a2b3c4"

# Show specific commit details
git log -1 1a2b3c4
```

## SHA Hash Properties

### Immutability

Once a SHA hash is created:

- Content cannot change without changing hash
- Provides data integrity verification
- Makes Git history tamper-evident
- Ensures consistency across repositories

### Uniqueness

- Astronomically unlikely to have collisions
- Git can detect hash collisions if they occur
- Each object has exactly one hash
- Hash serves as unique identifier

### Distribution Independence

- Same content produces same hash anywhere
- Repositories can verify object integrity
- Enables distributed development
- No central authority needed for IDs

## Working with SHA Hashes

### Hash Resolution

```bash
# Git accepts partial hashes
git show 1a2b    # If unambiguous

# Force minimum length
git config core.abbrev 8

# See what hash refers to
git cat-file -t 1a2b3c4  # Shows object type
git cat-file -s 1a2b3c4  # Shows object size
git cat-file -p 1a2b3c4  # Shows object content
```

### Hash Searching

```bash
# Find commit by partial hash
git log --oneline | grep 1a2b

# Find object type
git cat-file -t 1a2b3c4

# Verify object exists
git cat-file -e 1a2b3c4 && echo "exists" || echo "not found"
```

## SHA Hash Types

### Commit Hashes

```bash
# Commit object hash
commit 1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b

# Contains references to:
tree 5f6g7h8i9j...      # Snapshot hash
parent 9k8l7m6n5o...    # Parent commit hash
```

### Tree Hashes

```bash
# Directory snapshot hash
tree 5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4

# Contains:
blob 2a3b4c5d... file1.txt
blob 6e7f8g9h... file2.js
tree 1i2j3k4l... subdir/
```

### Blob Hashes

```bash
# File content hash
blob 2a3b4c5d6e7f8g9h0i1j2k3l4m5n6o7p8q9r0s1

# Same content = same hash regardless of:
# - File name
# - File location
# - Repository
```

## Practical SHA Hash Usage

### Code Review

```bash
# Reference specific commits in discussions
"Please review commit 1a2b3c4"

# Compare implementations
git diff 1a2b3c4..5d6e7f8
```

### Bug Tracking

```bash
# Identify problematic commit
git bisect bad 1a2b3c4

# Track when bug was introduced
git blame -C 1a2b3c4 -- file.js

# Cherry-pick fix
git cherry-pick 5d6e7f8
```

### Release Management

```bash
# Tag specific commit for release
git tag v1.0.0 1a2b3c4

# Build from specific commit
git checkout 1a2b3c4
make build
```

## SHA Hash Best Practices

### Using Hashes

- Use abbreviated hashes in documentation
- Include full hashes in automated systems
- Verify hash uniqueness in scripts
- Use descriptive references when possible

### Hash Management

- Don't manually type long hashes
- Use copy-paste for full hashes
- Leverage Git's tab completion
- Use `git log --oneline` for quick reference

### Security Considerations

- SHA-1 is being replaced with SHA-256
- Git detects collision attempts
- Hashes provide integrity verification
- Don't rely solely on partial hashes for security

## SHA Hash Limitations

### Hash Collisions

- Theoretically possible but extremely rare
- Git will detect and handle collisions
- Moving to SHA-256 for better security
- Not a practical concern for most users

### Hash Length

- 40 characters can be unwieldy
- Abbreviated hashes may become ambiguous
- Repository growth affects minimum length
- Balance between uniqueness and usability

## Migration to SHA-256

### Future of Git Hashes

- Git transitioning to SHA-256
- Better security properties
- Longer hashes (64 characters)
- Backward compatibility considerations

### Preparation

- Tools being updated for SHA-256
- Hash format will change
- Transition will be gradual
- Existing repositories will continue working

## Related Concepts

- [[Commit]] - Primary use of SHA hashes
- [[06-Internals|Git Internals]] - How hashes are stored
- [[git-rev-parse]] - Hash resolution command
- [[Repository]] - Contains hashed objects
- [[GitObjects]] - All use SHA hashes

## Quick Reference

| Command                  | Purpose                 |
| ------------------------ | ----------------------- |
| `git rev-parse HEAD`     | Get current commit hash |
| `git log --oneline`      | See abbreviated hashes  |
| `git show 1a2b3c4`       | Display object by hash  |
| `git cat-file -t <hash>` | Show object type        |
| `git cat-file -p <hash>` | Show object content     |
