---
id: FileTypes
aliases: []
tags: []
---

# File Types — Quick Reference

## File Type Characters

| Char | Type | Example |
|------|------|---------|
| `-` | Regular file | text, binary |
| `d` | Directory | folder |
| `l` | Symlink | shortcut |
| `c` | Character device | /dev/tty |
| `b` | Block device | /dev/sda |
| `p` | Named pipe (FIFO) | mkfifo |
| `s` | Socket | /var/run/*.sock |

## Common Extensions

| Extension | Meaning |
|-----------|---------|
| `.sh` | Shell script |
| `.conf` | Configuration |
| `.log` | Log file |
| `.service` | systemd unit |
| `.tar` | Tape archive |
| `.gz` | Gzip compressed |
| `.tar.gz` / `.tgz` | Tar + gzip |
| `.tar.bz2` | Tar + bzip2 |
| `.tar.xz` | Tar + xz |
| `.zip` | Zip archive |
| `.deb` | Debian package |

## Check File Type

```bash
file myfile                                # MIME type
ls -la                                     # Type char in listing
stat myfile                                # Full metadata
```

## Related Notes

- [[FileTypes]] — File types concept
- [[FilesystemHierarchy]] — FS layout
- [[ls]] — ls command
