---
id: git-check-ignore
aliases: []
tags: []
---

# git check-ignore

Debug `.gitignore` rules by showing whether a path is ignored and which rule matched.

## Syntax

```bash
git check-ignore [<options>] <path>...
git check-ignore [<options>] --stdin
```

## Description

`git check-ignore` tells you:

- is this file ignored?
- which ignore file + rule caused it (with `-v`)?

It’s the fastest way to debug confusing ignore behavior.

Related: [[GitIgnorePatterns]]

## Basic Usage

### Check a file

```bash
git check-ignore path/to/file
```

Exit status:

- `0` ignored
- `1` not ignored (no output)

### Show which rule matched (recommended)

```bash
git check-ignore -v path/to/file
```

Example output shape:

```txt
.gitignore:12:*.log    logs/app.log
```

### Check many files

```bash
git check-ignore -v file1 file2 dir/file3
```

## Options

### Read paths from stdin

```bash
printf "logs/app.log\n.env\n" | git check-ignore -v --stdin
```

### Null-terminated output (scripts)

```bash
git check-ignore -z --stdin
```

## Common Troubleshooting

### “Why is this not ignored?”

- pattern may be wrong (rooted `/` vs non-rooted)
- negation `!` might override earlier rules
- file may already be tracked (ignored rules don’t apply to tracked content)

If already tracked, remove from index:

```bash
git rm --cached path/to/file
```

See: [[git-rm]]

## Related Notes

- [[git-status]]
- [[git-rm]]
- [[GitIgnorePatterns]]
