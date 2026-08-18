---
id: du
aliases: []
tags: []
---

# du

Estimate file space usage.

## Syntax

```bash
du [options] [path]
```

## Common Usage

```bash
du -sh /var/log
```

```bash
du -h --max-depth=1 /
```

```bash
du -sh * | sort -hr | head
```

## Tips

- -s for summary, -h for human-readable, --max-depth for depth control

## Related Notes

- [[DiskManagement]]
