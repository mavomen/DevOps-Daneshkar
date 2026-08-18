---
id: uniq
aliases: []
tags: []
---

# uniq

Filter or report repeated lines.

## Syntax

```bash
uniq [options] [file]
```

## Common Usage

```bash
sort file | uniq
```

```bash
sort file | uniq -c
```

```bash
sort file | uniq -d
```

```bash
sort file | uniq -u
```

## Tips

- Must sort first. -c count, -d duplicates only, -u unique only

## Related Notes

- [[TextProcessing]]
