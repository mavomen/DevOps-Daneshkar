---
id: LogFormatting
aliases: []
tags: []
---

# Log Formatting

Quick patterns for getting useful `git log` output.

## Common log views

### One line per commit

```bash
git log --oneline
git log --oneline -n 30
```

### Graph view (branches/merges)

```bash
git log --graph --oneline --decorate --all
```

### Include file change stats

```bash
git log --stat
git log --shortstat
git log --name-only
```

### Filter by author

```bash
git log --author="Name"
```

### Filter by message

```bash
git log --grep="pattern"
```

### Filter by path

```bash
git log -- path/to/file
git log -- src/
git log -- '*.md'
```

### Search by content change

```bash
git log -S "string"
git log -G "regex"
```

## Custom pretty format

```bash
git log --pretty=format:"%h %ad %an %d %s" --date=short
```

Useful placeholders:

- `%H` full hash, `%h` short hash
- `%an` author name
- `%ad` author date
- `%s` subject
- `%d` decorations (branches/tags)

## Related Notes

- [[git-log]]
- [[GitHistory]]
