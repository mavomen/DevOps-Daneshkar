---
id: git-shortlog
aliases: []
tags: []
---

# git shortlog

Summarize `git log` output, typically grouped by author (great for release notes and contributor lists).

## Syntax

```bash
git shortlog [<options>] [<revision-range>] [--] [<path>...]
```

## Description

`git shortlog` is like `git log`, but aggregated:

- groups commits by author name (and optionally email)
- can show commit subjects, or only commit counts
- useful for changelogs and contributor stats

## Common Usage

### Show commits grouped by author (default)

```bash
git shortlog
```

### Show only counts per author (most common)

```bash
git shortlog -s
```

### Sort by number of commits (descending)

```bash
git shortlog -s -n
```

### Include email addresses

```bash
git shortlog -s -n -e
```

### Limit to a range (e.g., since last tag)

```bash
git shortlog -s -n v1.2.0..HEAD
```

### Limit by path (who changed a directory)

```bash
git shortlog -s -n -- src/
```

## Useful Options

- `-s` / `--summary`: show commit counts only
- `-n` / `--numbered`: sort by commit count
- `-e` / `--email`: show author emails
- `--no-merges`: ignore merge commits
- `--since=<date>` / `--until=<date>`: time filters (passed through log machinery)

Examples:

```bash
git shortlog -s -n --no-merges
git shortlog -s -n --since="2025-01-01" --until="2025-12-31"
```

## Related Notes

- [[git-log]]
- [[GitHistory]]
- [[Workflows/ReleaseWorkflow|Release Workflow]]
