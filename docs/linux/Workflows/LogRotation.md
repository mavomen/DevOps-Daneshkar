---
id: LogRotation
aliases: []
tags: []
---

# Log Rotation — Workflow

Managing log file growth and archival.

## Logrotate Configuration

```bash
# /etc/logrotate.d/myapp
/var/log/myapp/*.log {
    daily
    rotate 30
    compress
    delaycompress
    missingok
    notifempty
    create 0644 www-data www-data
    sharedscripts
    postrotate
        systemctl reload myapp > /dev/null 2>&1 || true
    endscript
}
```

## Directives

| Directive | Purpose |
|-----------|---------|
| `daily`/`weekly`/`monthly` | Rotation frequency |
| `rotate N` | Keep N old logs |
| `compress` | Compress old logs |
| `missingok` | Don't error if log missing |
| `notifempty` | Skip empty logs |
| `create` | Create new log with perms |
| `postrotate` | Command after rotation |

## Manual Rotation

```bash
# Force rotation now
logrotate -f /etc/logrotate.d/myapp

# Test without rotating
logrotate -d /etc/logrotate.d/myapp

# Check status
cat /var/lib/logrotate/status
```

## Common Log Locations

| Log | Purpose |
|-----|---------|
| `/var/log/syslog` | System messages |
| `/var/log/auth.log` | Authentication |
| `/var/log/kern.log` | Kernel messages |
| `/var/log/dmesg` | Boot messages |
| `/var/log/nginx/` | Nginx logs |
| `/var/log/journal/` | systemd journal |

## Related Notes

- [[LogSystem]] — System logging
- [[FileOrganization]] — Directory structure
- [[DiskManagement]] — Disk space management
