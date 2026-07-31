---
id: GitAttributes
aliases: []
tags: []
---

# Git Attributes

`.gitattributes` controls how Git treats paths (text vs binary, line endings, diff/merge drivers, export rules, etc.).

## Suggested Aliases (optional)

- `Git Attributes`

## Why It Matters

- enforce consistent line endings across platforms
- improve diffs for certain file types
- define merge behavior for generated files
- mark binaries to avoid broken diffs

## Basic `.gitattributes` (Recommended Baseline)

Create `.gitattributes` at repo root:

```gitattributes
# Auto-detect text files and normalize
* text=auto

# Enforce LF for shells
*.sh text eol=lf

# Enforce CRLF for Windows scripts (optional)
*.bat text eol=crlf
*.ps1 text eol=crlf

# Treat images as binary
*.png binary
*.jpg binary
*.jpeg binary
```

## Line Endings vs autocrlf

- `core.autocrlf` is a client preference (user config)
- `.gitattributes` is a repo policy (shared)

If your team needs strict consistency, prefer `.gitattributes` as the source of truth.

See: [[GitConfiguration]]

## Custom diff drivers (example)

Format JSON before diff:

```gitattributes
*.json diff=json
```

Then configure:

```bash
git config diff.json.textconv "python -m json.tool"
```

## Custom merge drivers (example idea)

Ignore merges for generated files:

```gitattributes
*.generated merge=ours
```

Then configure driver:

```bash
git config merge.ours.driver true
```

## Related Notes

- [[GitConfiguration]]
- [[git-diff]]
- [[git-merge]]
