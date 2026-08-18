---
id: FileOrganization
aliases: []
tags: []
---

# Linux File Organization — Best Practices

Standard directory layout and naming conventions.

## FHS Standard

```
/           Root
├── bin/    Essential user binaries
├── sbin/   System binaries
├── etc/    Configuration files
├── var/    Variable data (logs, caches)
├── tmp/    Temporary files
├── home/   User home directories
├── root/   Root user home
├── dev/    Device files
├── proc/   Process info (virtual)
├── sys/    System info (virtual)
├── mnt/    Temporary mounts
├── opt/    Third-party software
└── usr/    User programs and data
```

## Best Practices

- **Don't put custom files** in `/bin`, `/sbin`, `/usr` — use `/usr/local`
- **Use `/opt`** for self-contained third-party apps
- **Keep `/tmp` clean** — scripts should clean up
- **Log rotation** — don't let `/var/log` grow unbounded
- **Config in `/etc`** — never hardcode config paths
- **Data in `/var`** — separate data from code

## Naming Conventions

```
# Config files
/etc/nginx/nginx.conf
/etc/systemd/system/myapp.service

# Logs
/var/log/myapp/error.log
/var/log/myapp/access.log

# Data
/var/lib/myapp/
/var/cache/myapp/

# PID files
/var/run/myapp.pid
```

## Related Notes

- [[FilesystemHierarchy]] — FS structure
- [[DiskManagement]] — Storage management
- [[BackupStrategies]] — Backup planning
