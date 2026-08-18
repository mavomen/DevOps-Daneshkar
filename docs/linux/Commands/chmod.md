---
id: chmod
aliases: []
tags: []
---

# chmod

Change file permissions.

## Syntax

```bash
chmod [mode] file...
```

## Common Usage

```bash
chmod 755 script.sh
```

```bash
chmod u+x script.sh
```

```bash
chmod -R 644 dir/
```

```bash
chmod go-w file
```

## Tips

- Use octal (755) or symbolic (u+x, go-w) modes

## Related Notes

- [[LinuxPermissions]]
