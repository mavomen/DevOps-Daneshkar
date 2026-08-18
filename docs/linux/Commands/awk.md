---
id: awk
aliases: []
tags: []
---

# awk

Pattern scanning and processing language.

## Syntax

```bash
awk 'pattern {action}' file
```

## Common Usage

```bash
awk '{print $1}' file
```

```bash
awk -F: '{print $1, $3}' /etc/passwd
```

```bash
awk '/error/ {print NR, $0}' log
```

## Tips

- $0=whole line, $1-first field, NR=line number, NF=field count

## Related Notes

- [[TextProcessing]]
