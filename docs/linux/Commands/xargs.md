---
id: xargs
aliases: []
tags: []
---

# xargs

Build and execute commands from stdin.

## Syntax

```bash
xargs [options] [command]
```

## Common Usage

```bash
find . -name '*.tmp' | xargs rm
```

```bash
cat urls.txt | xargs -I{} curl -O {}
```

```bash
echo {1..10} | xargs -I{} mkdir dir{}
```

## Tips

- -I{} for placeholder, -n for args per command, -0 for null-delimited input

## Related Notes

- [[ShellBasics]]
