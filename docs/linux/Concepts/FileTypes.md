---
id: FileTypes
aliases: []
tags: []
---

# File Types

Linux treats everything as a file. There are several types.

## File Type Indicators

| Indicator | Type | Example |
|-----------|------|---------|
| `-` | Regular file | Text, binary, image |
| `d` | Directory | `/home`, `/etc` |
| `l` | Symbolic link | Shortcut to another file |
| `c` | Character device | Keyboard, terminal (`/dev/tty`) |
| `b` | Block device | Hard disk, SSD (`/dev/sda`) |
| `p` | Named pipe (FIFO) | IPC between processes |
| `s` | Socket | Network/IPC socket |

## Identify Types

```bash
ls -la /path/                               # First char shows type
file /path/to/file                          # Detailed type info
stat /path/to/file                          # Full metadata
```

## Special Files

| Path | Type | Purpose |
|------|------|---------|
| `/dev/null` | Char device | Discards all output |
| `/dev/zero` | Char device | Infinite stream of zeros |
| `/dev/random` | Char device | Random data (blocking) |
| `/dev/urandom` | Char device | Random data (non-blocking) |
| `/dev/stdin` | Link | Standard input |
| `/dev/stdout` | Link | Standard output |

## Symbolic vs Hard Links

```bash
ln -s target link_name                      # Symbolic link (can cross filesystems)
ln target link_name                         # Hard link (same inode)
readlink -f link_name                       # Resolve symlink
```

| Property | Hard Link | Symbolic Link |
|----------|-----------|---------------|
| Cross filesystem | No | Yes |
| Points to inode | Yes | No (path) |
| Survives target delete | Yes | No (broken) |
| Can link directories | No | Yes |

## Related Notes

- [[FilesystemHierarchy]] — Directory structure
- [[LinuxPermissions]] — Permissions
- [[DiskManagement]] — Block devices
