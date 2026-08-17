---
id: git-tag
aliases: []
tags: []
---

# git tag

Create, list, and manage tags (commonly used for releases).

## Syntax

```bash
git tag
git tag <name> [<commit>]
git tag -a <name> -m "<message>" [<commit>]
git tag -d <name>
git show <tag>
```

## Description

Tags are named pointers to commits.

Two common types:

- **lightweight tag**: just a pointer (like a named ref)
- **annotated tag**: stored as a Git object with metadata/message (recommended for releases)

Tags are often used for versioned releases (e.g., `v1.2.0`).

Related concepts:

- [[Commit]]
- [[SHAHash]]
- [[GitObjects]]

## Basic Usage

### List tags

```bash
git tag
```

### Create lightweight tag (at HEAD)

```bash
git tag v1.0.0
```

### Create annotated tag (recommended)

```bash
git tag -a v1.0.0 -m "Release v1.0.0"
```

### Tag a specific commit

```bash
git tag -a v1.0.0 -m "Release v1.0.0" <commit-hash>
```

### Inspect a tag

```bash
git show v1.0.0
```

### Delete a local tag

```bash
git tag -d v1.0.0
```

## Remote Tags

### Push a tag

```bash
git push origin v1.0.0
```

### Push all tags

```bash
git push origin --tags
```

### Delete a remote tag

```bash
git push origin --delete v1.0.0
```

## Troubleshooting

### “I tagged the wrong commit”

- delete and recreate (if not shared), or coordinate with your team if already pushed.

```bash
git tag -d v1.0.0
git tag -a v1.0.0 -m "Correct" <correct-commit>
git push --force origin v1.0.0
```

> Only force if your team policy allows; otherwise create a new version tag.

## Examples

```bash
# Tag a release
git switch main
git pull --ff-only
git tag -a v2.1.0 -m "Release v2.1.0"
git push origin main --tags
```


## Related Notes

- [[git-log]] / [[git-show]] - find and verify target commit
- [[git-push]] - publish tags
- [[git-checkout]] - you can checkout a tag (detached HEAD)
