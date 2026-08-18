---
id: sed
aliases: []
tags: []
---

# sed

Stream editor for filtering and transforming text.

## Syntax

```bash
sed [options] 'command' file
```

## Common Usage

```bash
sed 's/old/new/g' file
```

```bash
sed -i 's/old/new/g' file
```

```bash
sed -n '5,10p' file
```

```bash
sed '/^#/d' file
```

## Tips

- -i for in-place edit, s/old/new/g for replace, d for delete, p for print

## Related Notes

- [[TextProcessing]]
