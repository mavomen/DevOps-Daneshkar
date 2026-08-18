---
id: wc
aliases: []
tags: []
---

# wc

Word, line, character, byte count.

## Syntax

```bash
wc [options] [file]
```

## Common Usage

```bash
wc -l file.txt
```

```bash
wc -w file.txt
```

```bash
find . -name '*.py' | wc -l
```

## Tips

- -l lines, -w words, -c bytes, -m characters

## Related Notes

- [[TextProcessing]]
