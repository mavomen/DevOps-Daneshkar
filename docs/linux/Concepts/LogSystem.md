---
id: LogSystem
aliases: []
tags: []
---

# Log System

Linux logging: journald, syslog, and log files.

## journald (systemd)

```bash
journalctl                                  # All logs
journalctl -b                               # Current boot
journalctl -b -1                            # Previous boot
journalctl -u nginx                         # Specific unit
journalctl -f                               # Follow (real-time)
journalctl --since "1 hour ago"             # Time range
journalctl -p err                           # Priority filter
journalctl -k                               # Kernel messages
```

## Syslog (Debian/Ubuntu)

| File | Content |
|------|---------|
| `/var/log/syslog` | All system messages |
| `/var/log/auth.log` | Authentication events |
| `/var/log/dpkg.log` | Package installations |
| `/var/log/kern.log` | Kernel messages |
| `/var/log/daemon.log` | Daemon messages |

## Logrotate

Manages log rotation to prevent disk filling up.

```bash
cat /etc/logrotate.conf                     # Main config
ls /etc/logrotate.d/                        # Per-app configs
logrotate -d /etc/logrotate.conf            # Test (dry run)
logrotate -f /etc/logrotate.conf            # Force rotation
```

## Important Log Files

| File | Content |
|------|---------|
| `/var/log/boot.log` | Boot messages |
| `/var/log/dmesg` | Kernel ring buffer |
| `/var/log/faillog` | Failed login attempts |
| `/var/log/lastlog` | Last login per user |
| `/var/log/wtmp` | Login/logout history |

## Related Notes

- [[journalctl]] — journalctl command
- [[AuthenticationLogs]] — Auth log analysis
- [[LogAnalysis]] — Log troubleshooting
- [[LogRotation]] — Log rotation workflows
