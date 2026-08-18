---
id: chown
aliases: []
tags: []
---

# chown

Change file owner and group.

## Syntax

```bash
chown [owner][:group] file...
```

## Common Usage

```bash
chown user:group file
```

```bash
chown -R www-data:www-data /var/www
```

```bash
chown :docker file
```

## Tips

- -R for recursive, use :group to change only group

## Related Notes

- [[LinuxPermissions]]
