---
id: git-blame
aliases: []
tags: []
---

# git blame

Show who last modified each line of a file (line-by-line attribution).

## Syntax

```bash
git blame [<options>] [--] <file>
```

## Description

`git blame` annotates a file by showing, for each line, the commit (and author) that last changed it. It’s one of the fastest ways to answer:

- “When did this line change?”
- “Which commit introduced this behavior?”
- “Who touched this code last (and what was the context)?”

Related concept:

- [[GitHistory]]

## Basic Usage

### Blame a file

```bash
git blame path/to/file
```

### Show blame for a line range

```bash
git blame -L 10,40 path/to/file
# blame only lines 10..40
```

### Ignore whitespace-only changes

```bash
git blame -w path/to/file
```

### Follow moves/copies across lines

Useful when code moved between files or was refactored:

```bash
# detect moved/copied lines within the file
git blame -M path/to/file

# detect moved/copied lines across files as well
git blame -C -C path/to/file
```

## Output Interpretation

Typical output looks like:

```txt
1a2b3c4d (Alice 2024-01-15 12:34:56 +0330  10) const x = 10;
```

- `1a2b3c4d` = commit hash (abbrev)
- `(Alice ...)` = author and timestamp
- `10` = line number in the current file
- the rest is the current content of that line

## Practical Workflows

### From blame → show the commit

```bash
git blame -L 120,140 path/to/file
git show <commit-hash>
```

### Blame with context from history

```bash
git log --oneline -- path/to/file
git show <commit-hash> -- path/to/file
```

## Troubleshooting / Notes

- If a file was renamed, `git blame` won’t automatically follow renames; you may need to inspect history with:
  - `git log --follow -- path/to/file` (see [[git-log]])

## Related Notes

- [[git-log]] - explore file history
- [[git-show]] - inspect a specific commit
- [[git-diff]] - compare versions
- [[git-bisect]] - find which commit introduced a bug (automated)
