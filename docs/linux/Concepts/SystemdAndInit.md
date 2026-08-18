---
id: SystemdAndInit
aliases: []
tags: []
---

# Systemd & Init

systemd is the init system and service manager on most modern Linux distros.

## Key Concepts

| Concept | Description |
|---------|-------------|
| Unit | Resource managed by systemd (service, timer, mount, socket) |
| Target | Group of units (replaces runlevels) |
| Service | Daemon or background process |
| Timer | Cron replacement (scheduled tasks) |
| Socket | IPC/socket activation |

## Common Targets

| Target | Runlevel Equivalent | Purpose |
|--------|---------------------|---------|
| `multi-user.target` | 3 | Multi-user, no GUI |
| `graphical.target` | 5 | Multi-user + GUI |
| `rescue.target` | 1 | Single-user/recovery |
| `emergency.target` | — | Minimal shell, root fs read-only |
| `poweroff.target` | 0 | Shutdown |
| `reboot.target` | 6 | Reboot |

## Commands

```bash
systemctl start nginx                       # Start service
systemctl stop nginx                        # Stop service
systemctl restart nginx                     # Restart service
systemctl reload nginx                      # Reload config
systemctl enable nginx                      # Start on boot
systemctl disable nginx                     # Don't start on boot
systemctl status nginx                      # Service status
systemctl is-active nginx                   # Check if running
systemctl is-enabled nginx                  # Check if enabled

systemctl list-units --type=service         # All services
systemctl list-unit-files --type=service    # All unit files
systemctl list-timers                       # All timers

systemctl get-default                       # Current target
systemctl set-default multi-user.target     # Set default target

systemctl daemon-reload                     # Reload unit files
```

## Unit Files

```ini
# /etc/systemd/system/myapp.service
[Unit]
Description=My Application
After=network.target

[Service]
Type=simple
User=www-data
ExecStart=/usr/bin/myapp --config /etc/myapp.conf
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

## Related Notes

- [[ServiceManagement]] — Service workflows
- [[BootProcess]] — Boot sequence
- [[systemctl]] — systemctl command
