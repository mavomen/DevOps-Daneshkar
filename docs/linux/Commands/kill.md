---
id: kill
aliases: []
tags: []
---

# kill

Send signals to processes.

## Syntax

```bash
kill [options] pid...
```

## Common Usage

```bash
kill 1234
```

```bash
kill -9 1234
```

```bash
kill -HUP 1234
```

```bash
killall nginx
```

## Tips

- Default signal is SIGTERM (15). Use -9 (SIGKILL) only as last resort

## Related Notes

- [[SignalsAndTraps]]
