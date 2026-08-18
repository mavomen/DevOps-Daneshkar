---
id: mount
aliases: []
tags: []
---

# mount

Mount a filesystem.

## Syntax

```bash
mount [options] device mountpoint
```

## Common Usage

```bash
mount /dev/sdb1 /mnt/data
```

```bash
mount -o loop image.iso /mnt/iso
```

```bash
mount -t nfs server:/share /mnt/nfs
```

## Tips

- -o for options (ro, rw, noexec), -t for filesystem type

## Related Notes

- [[DiskManagement]]
