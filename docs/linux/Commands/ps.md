---
id: ps
aliases: []
tags: []
---

# ps

Report current processes.

## Syntax

```bash
ps [options]
```

## Common Usage

```bash
ps aux
```

```bash
ps aux | grep nginx
```

```bash
ps -ef | grep java
```

```bash
ps -eo pid,ppid,user,%cpu,%mem,cmd | head
```

## Tips

- aux shows all users, -ef shows full format, combine with grep to filter

## Related Notes

- [[ProcessManagement]]
