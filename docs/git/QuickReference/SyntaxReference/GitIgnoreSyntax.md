---
id: GitIgnoreSyntax
aliases: []
tags: []
---

# GitIgnore Syntax

Quick reference for `.gitignore` patterns.

## Basics

- one pattern per line
- `#` starts a comment
- blank lines are ignored

## Wildcards

| Pattern     | Meaning                              |
| ----------- | ------------------------------------ |
| `*.log`     | any `.log` file                      |
| `build/`    | directory named build anywhere       |
| `/build/`   | build directory at repo root only    |
| `**/build/` | any build directory (recursive glob) |

## Negation

Un-ignore a path:

```txt
*.log
!important.log
```

## Anchoring (rooted patterns)

```txt
/config.json
```

Matches only `config.json` at repo root.

## Directory-only

```txt
node_modules/
```

## Debug ignores

```bash
git check-ignore -v path/to/file
```

## Related Notes

- [[GitIgnorePatterns]]
- [[git-rm]]
