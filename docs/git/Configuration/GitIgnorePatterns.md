---
id: GitIgnorePatterns
aliases: []
tags: []
---

# GitIgnore Patterns

Use `.gitignore` (and related ignore mechanisms) to stop Git from tracking files you don’t want in history.

## Suggested Aliases (optional)

If your vault already links to `[[GitIgnore Patterns]]` (with a space), add alias:

- `GitIgnore Patterns`

## Ignore Mechanisms (Priority-ish)

1. `.gitignore` in repo (tracked, shared)
2. `.git/info/exclude` (local to repo, not shared)
3. global ignore via `core.excludesfile` (user-wide)

## Basic `.gitignore`

Create `.gitignore` in repo root:

```txt
# OS
.DS_Store
Thumbs.db

# Logs
*.log

# Dependencies
node_modules/

# Secrets
.env
```

## Common Patterns

| Pattern          | Meaning                         |
| ---------------- | ------------------------------- |
| `*.log`          | ignore all `.log` files         |
| `build/`         | ignore directory named build    |
| `/build/`        | ignore build only at repo root  |
| `!important.log` | un-ignore one path              |
| `**/*.tmp`       | ignore tmp in any subdir (glob) |

## Global Ignore (your machine)

Set a global ignore file:

```bash
git config --global core.excludesfile ~/.config/git/ignore
```

Example `~/.config/git/ignore`:

```txt
.DS_Store
*.swp
.idea/
.vscode/
```

## Important: Ignoring ≠ Untracking

If a file is already tracked, adding it to `.gitignore` won’t remove it from history.

To stop tracking but keep the file locally:

```bash
git rm --cached path/to/file
git commit -m "Stop tracking file"
```

## Debugging Ignore Rules

```bash
git check-ignore -v path/to/file
```

## Related Notes

- [[GitConfiguration]]
- [[git-rm]]
- [[git-status]]
- [[git-check-ignore]] (optional future note)
