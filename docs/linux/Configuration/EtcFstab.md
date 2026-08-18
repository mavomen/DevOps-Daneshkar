---
id: EtcFstab
aliases: []
tags: []
---

# /etc/fstab — Filesystem Mount Table

Defines which filesystems are mounted at boot.

## Format

```
<device>  <mount>  <type>  <options>  <dump>  <pass>
```

| Field | Meaning |
|-------|---------|
| `device` | Device path or UUID |
| `mount` | Mount point |
| `type` | Filesystem type (ext4, xfs, etc.) |
| `options` | Mount options |
| `dump` | Backup flag (0=never, 1=daily) |
| `pass` | fsck order (0=skip, 1=root, 2=others) |

## Example

```
# <device>                               <mount>  <type>  <options>        <dump> <pass>
UUID=abc123-def456                       /        ext4    errors=remount-ro 0      1
UUID=789abc-def012                       /home    ext4    defaults           0      2
UUID=111aaa-222bbb                       none     swap    sw                 0      0
//nas/share                              /mnt/nas cifs    credentials=/etc/smb,uid=1000  0  0
```

## Common Operations

```bash
cat /etc/fstab                            # View mount table
lsblk -f                                  # Device UUIDs and types
sudo mount -a                             # Mount all from fstab
sudo umount /mnt/data                     # Unmount
```

## Common Options

| Option | Meaning |
|--------|---------|
| `defaults` | rw, suid, dev, exec, auto, nouser, async |
| `noexec` | Prevent program execution |
| `nosuid` | Ignore SUID/SGID bits |
| `nodev` | No device files |
| `ro` | Read-only |

## Related Notes

- [[DiskManagement]] — Disk and partition management
- [[mount]] — mount command
- [[BackupAndRestore]] — Backup workflows
