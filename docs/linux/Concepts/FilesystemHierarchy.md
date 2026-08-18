---
id: FilesystemHierarchy
aliases: []
tags: []
---

# Filesystem Hierarchy

Linux follows a standard directory layout defined by the Filesystem Hierarchy Standard (FHS).

## Top-Level Directories

| Directory | Purpose |
|-----------|---------|
| `/` | Root — everything starts here |
| `/bin` | Essential user binaries (ls, cp, cat) |
| `/sbin` | System binaries (fdisk, mount, iptables) |
| `/etc` | System configuration files |
| `/home` | User home directories |
| `/root` | Root user's home directory |
| `/var` | Variable data (logs, caches, mail) |
| `/tmp` | Temporary files (cleared on reboot) |
| `/usr` | User programs and libraries |
| `/opt` | Optional/third-party software |
| `/dev` | Device files (null, zero, sda) |
| `/proc` | Process and kernel info (virtual) |
| `/sys` | Kernel and driver info (virtual) |
| `/mnt` | Temporary mount points |
| `/media` | Removable media mount points |
| `/boot` | Kernel and bootloader files |
| `/lib` | Shared libraries for /bin and /sbin |
| `/srv` | Service data (web, FTP) |

## Key Subdirectories

```bash
/etc/passwd          # User accounts
/etc/shadow          # Password hashes
/etc/group           # Groups
/etc/fstab           # Mount points
/etc/ssh/            # SSH configuration
/etc/systemd/        # Service unit files
/var/log/            # Log files
/var/cache/          # Package cache
/tmp/                # Temporary files
```

## Virtual Filesystems

| Path | Type | Content |
|------|------|---------|
| `/proc` | procfs | Running processes, kernel params |
| `/sys` | sysfs | Devices, drivers, kernel modules |
| `/dev` | devfs | Device nodes (null, zero, random) |

## Related Notes

- [[DiskManagement]] — Disk and partition management
- [[LinuxPermissions]] — File permissions
- [[FileTypes]] — Types of files
