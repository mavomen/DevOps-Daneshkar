---
id: cut
aliases: []
tags: []
---

# cut

Remove sections from lines of files.

## Syntax

```bash
cut [options] [file]
```

## Common Usage

```bash
cut -d: -f1 /etc/passwd
```

```bash
cut -c1-10 file.txt
```

```bash
cut -d',' -f2,4 data.csv
```

## Tips

- -d delimiter, -f fields, -c characters

## Related Notes

- [[TextProcessing]]
