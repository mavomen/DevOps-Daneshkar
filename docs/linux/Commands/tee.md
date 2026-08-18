---
id: tee
aliases: []
tags: []
---

# tee

Read from stdin and write to stdout and files.

## Syntax

```bash
tee [options] [file]
```

## Common Usage

```bash
echo 'log' | tee file.txt
```

```bash
command | tee -a logfile
```

```bash
command | tee file1 file2
```

## Tips

- -a to append, -i to ignore interrupts. Useful for logging while piping

## Related Notes

- [[ShellBasics]]
