---
id: DiskFull
aliases: []
tags: []
---

# Disk Full — Troubleshooting

Diagnosing and resolving disk space issues.

## Quick Diagnosis

```bash
df -h                                      # Overall usage
df -ih                                     # Inode usage (full = can't create files)
du -sh /* 2>/dev/null | sort -hr | head   # Top directories
du -sh /var/log/* | sort -hr | head       # Log sizes
```

## Common Causes

| Cause | Fix |
|-------|-----|
| Log files growing | Rotate logs, delete old |
| /tmp full | Clean temp files |
| Package cache | `apt clean` |
| Old kernels | `apt autoremove` |
| Docker images | `docker system prune -a` |
| Journal logs | `journalctl --vacuum-size=100M` |

## Find Large Files

```bash
find / -type f -size +100M -exec ls -lh {} \; 2>/dev/null
find /var -type f -name "*.log" -size +50M
find /tmp -type f -mtime +7 -delete
```

## Clean Commands

```bash
# Package manager
apt clean && apt autoremove -y

# Journal
journalctl --vacuum-size=100M
journalctl --vacuum-time=7d

# Docker
docker system prune -a --volumes

# Old logs
find /var/log -name "*.gz" -delete
find /var/log -name "*.old" -delete

# Snapshots (if applicable)
btrfs subvolume list / | grep snapshots
```

## Related Notes

- [[DiskManagement]] — Disk concepts
- [[LogSystem]] — Log management
- [[LogRotation]] — Log rotation
- [[FileOrganization]] — Directory structure
