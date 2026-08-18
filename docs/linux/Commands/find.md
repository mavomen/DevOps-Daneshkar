---
id: find
aliases: []
tags: []
---

# find

Search for files by criteria.

## Syntax

```bash
find [path] [expression]
```

## Common Usage

```bash
find . -name '*.py'
```

```bash
find / -type f -size +100M
```

```bash
find . -mtime -7
```

```bash
find . -name '*.log' -delete
```

## Tips

- -name (case-sensitive), -iname (case-insensitive), -type f/d/l, -size, -mtime, -exec

## Related Notes

- [[FilesystemHierarchy]]
