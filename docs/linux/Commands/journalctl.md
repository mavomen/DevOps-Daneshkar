---
id: journalctl
aliases: []
tags: []
---

# journalctl

Query systemd journal logs.

## Syntax

```bash
journalctl [options]
```

## Common Usage

```bash
journalctl -u nginx
```

```bash
journalctl -f
```

```bash
journalctl --since '1 hour ago'
```

```bash
journalctl -p err -b
```

## Tips

- -u for unit, -f for follow, -p for priority, -b for current boot

## Related Notes

- [[LogSystem]]
