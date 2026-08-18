---
id: LogAnalysis
aliases: []
tags: []
---

# Log Analysis — Troubleshooting

Finding and interpreting system logs.

## Key Log Files

| File | Content |
|------|---------|
| `/var/log/syslog` | System messages |
| `/var/log/auth.log` | Authentication |
| `/var/log/kern.log` | Kernel messages |
| `/var/log/dmesg` | Boot messages |
| `/var/log/nginx/` | Nginx logs |
| `/var/log/postgresql/` | PostgreSQL logs |

## Search Logs

```bash
# Grep patterns
grep -i error /var/log/syslog              # Case-insensitive
grep -i "failed\|error\|fatal" /var/log/syslog
grep -E "^[0-9]{4}-[0-9]{2}" /var/log/syslog  # Timestamped lines

# By time range
grep "2025-01-15" /var/log/syslog
awk '/2025-01-15 10:00/,/2025-01-15 11:00/' /var/log/syslog

# Last N lines
tail -100 /var/log/syslog
tail -f /var/log/syslog                     # Follow in real-time
```

## systemd Journal

```bash
journalctl                                 # All logs
journalctl -u nginx                        # Specific unit
journalctl -f                              # Follow all
journalctl -p err                          # Errors only
journalctl --since "1 hour ago"            # Time range
journalctl --since "2025-01-15 10:00" --until "2025-01-15 11:00"
journalctl -b                              # Current boot
journalctl -b -1                           # Previous boot
```

## Log Patterns

```bash
# Count errors per hour
grep "error" /var/log/syslog | awk '{print $3}' | sort | uniq -c | sort -rn

# Top error messages
grep -i error /var/log/syslog | awk '{$1=$2=$3=""; print}' | sort | uniq -c | sort -rn | head
```

## Related Notes

- [[LogSystem]] — Logging concepts
- [[LogRotation]] — Log rotation
- [[journalctl]] — Journal command
- [[SystemStatus]] — System investigation
