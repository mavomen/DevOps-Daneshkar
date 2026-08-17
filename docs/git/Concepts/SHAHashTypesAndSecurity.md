---
id: SHAHashTypesAndSecurity
aliases: []
tags: []
---

# SHA Hash Types & Security

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

## Related Notes

- [[SHAHash]] — Core concepts
- [[SHAHashTypesAndSecurity]] — This note
