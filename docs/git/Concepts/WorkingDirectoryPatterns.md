---
id: WorkingDirectoryPatterns
aliases: []
tags: []
---

# Working Directory Patterns

## Working Directory Patterns

### Feature Development

```bash
# Start clean
git status

# Create feature branch
git switch -c feature/new-feature

# Make changes
# Edit files...

# Review changes
git diff
git status

# Stage and commit
git add .
git commit -m "Implement new feature"
```

### Experimental Changes

```bash
# Save current work
git stash

# Try experimental changes
# Edit files...

# If experiment works
git add .
git commit -m "Add experimental feature"

# If experiment fails
git restore .
git stash pop  # Restore previous work
```

## Common Working Directory Issues

### Conflicting Changes

When [[git-pull]] or [[git-merge]] creates conflicts:

- Conflict markers appear in files
- Working directory contains both versions
- Must manually resolve conflicts
- See [[MergeConflicts]]

### Accidental Changes

```bash
# Restore accidentally deleted file
git restore deleted-file.txt

# Restore accidentally modified file
git restore modified-file.txt

# Restore entire directory
git restore src/
```

### Large Files

- Avoid committing large binary files
- Use [[GitIgnorePatterns]] for build outputs
- Consider Git LFS for necessary large files
- See [[LargeFileIssues]]

## Working Directory Tools

### IDE Integration

Most editors provide Git integration:

- Visual diff displays
- File status indicators
- Staging area management
- Commit tools

### Command Line Tools

```bash
# Enhanced status
git status --short --branch

# Tree view of changes
tree -a -I '.git'

# Watch for file changes
watch git status
```

## Troubleshooting

### Permission Issues

```bash
# Fix file permissions
chmod 644 filename.txt

# See file permissions
ls -la
```

### File System Issues

- Check disk space: `df -h`
- Verify file system integrity
- Ensure proper file encoding
- Handle line ending differences

## Related Notes

- [[WorkingDirectory]] — Core concepts
- [[WorkingDirectoryPatterns]] — This note
