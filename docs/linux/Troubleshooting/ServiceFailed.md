---
id: ServiceFailed
aliases: []
tags: []
---

# Service Failed — Troubleshooting

Diagnosing failed systemd services.

## Quick Diagnosis

```bash
systemctl status myapp -l                  # Full status + recent logs
journalctl -u myapp -n 100 --no-pager     # Last 100 log lines
journalctl -u myapp --since "10 min ago"  # Recent logs
systemctl show myapp                       # All properties
```

## Common Causes

| Issue | Check |
|-------|-------|
| Config error | `systemctl status` shows config parse error |
| Port in use | `ss -tlnp \| grep PORT` |
| Permission denied | Check user/group in service file |
| Missing dependency | Check `After=` / `Wants=` |
| Crash loop | `Restart=on-failure` + `RestartSec=` |

## Fix Config Issues

```bash
# Test config
myapp --configtest                         # Nginx, etc.
systemd-analyze verify /etc/systemd/system/myapp.service

# Check syntax
journalctl -u myapp | grep -i "error\|failed"
```

## Reset Failed State

```bash
systemctl reset-failed myapp               # Clear failed state
systemctl restart myapp                    # Try again
```

## Resource Limits

```bash
# Check limits
systemctl show myapp | grep Limit

# Increase limits
# /etc/systemd/system/myapp.service.d/limits.conf
[Service]
LimitNOFILE=65536
LimitNPROC=4096
LimitCORE=infinity
```

## Related Notes

- [[SystemdAndInit]] — systemd concepts
- [[ServiceManagement]] — Service workflow
- [[LogSystem]] — Journal logs
- [[ProcessManagement]] — Process investigation
