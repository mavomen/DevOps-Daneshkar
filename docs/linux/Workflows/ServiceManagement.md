---
id: ServiceManagement
aliases: []
tags: []
---

# Service Management — Workflow

Creating, enabling, and managing systemd services.

## Create Custom Service

```bash
# 1. Create service file
cat > /etc/systemd/system/myapp.service << 'EOF'
[Unit]
Description=My Application
After=network.target
Wants=postgresql.service

[Service]
Type=simple
User=deploy
Group=deploy
WorkingDirectory=/opt/myapp
ExecStart=/opt/myapp/bin/start
ExecStop=/opt/myapp/bin/stop
Restart=on-failure
RestartSec=5

# Environment
EnvironmentFile=/etc/myapp/env

# Security
NoNewPrivileges=true
ProtectSystem=strict
ProtectHome=true
ReadWritePaths=/var/lib/myapp /var/log/myapp

[Install]
WantedBy=multi-user.target
EOF
```

## Enable & Start

```bash
systemctl daemon-reload
systemctl enable myapp                     # Start at boot
systemctl start myapp                      # Start now
systemctl status myapp                     # Check status
```

## Manage

```bash
systemctl restart myapp                    # Restart
systemctl stop myapp                       # Stop
systemctl disable myapp                    # Remove from boot
systemctl is-enabled myapp                 # Check if enabled
systemctl is-active myapp                  # Check if running
```

## Troubleshoot

```bash
systemctl status myapp -l                  # Full status
journalctl -u myapp -f                     # Follow logs
journalctl -u myapp --since "1 hour ago"   # Recent logs
systemctl show myapp                       # Internal properties
```

## Related Notes

- [[SystemdAndInit]] — systemd concepts
- [[ProcessManagement]] — Process control
- [[LogSystem]] — Journal logs
