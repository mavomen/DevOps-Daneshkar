---
id: tail
aliases: []
tags: []
---

# tail

Output the last lines of a file.

## Syntax

```bash
tail [options] [file]
```

## Common Usage

```bash
tail -20 file.txt
```

```bash
tail -f /var/log/syslog
```

```bash
tail -f --pid=PID logfile
```

## Tips

- -f for follow (live), -n for lines, --pid stops when process dies

## Related Notes

- [[LogSystem]]
