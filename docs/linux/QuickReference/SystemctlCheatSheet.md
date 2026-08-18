---
id: SystemctlCheatSheet
aliases: []
tags: []
---

# Systemctl Cheat Sheet — Quick Reference

## Service Management

| Command | Description |
|---------|-------------|
| `systemctl start svc` | Start service |
| `systemctl stop svc` | Stop service |
| `systemctl restart svc` | Restart service |
| `systemctl reload svc` | Reload config |
| `systemctl status svc` | Show status |
| `systemctl is-active svc` | Check if running |
| `systemctl is-enabled svc` | Check if enabled at boot |

## Enable / Disable

| Command | Description |
|---------|-------------|
| `systemctl enable svc` | Start at boot |
| `systemctl disable svc` | Don't start at boot |
| `systemctl enable --now svc` | Enable + start |
| `systemctl mask svc` | Prevent starting |
| `systemctl unmask svc` | Allow starting |

## Listing

| Command | Description |
|---------|-------------|
| `systemctl list-units` | Loaded units |
| `systemctl list-units --type=service` | Services only |
| `systemctl list-units --state=running` | Running only |
| `systemctl list-unit-files` | Available units |
| `systemctl list-dependencies svc` | Dependency tree |

## System Control

| Command | Description |
|---------|-------------|
| `systemctl reboot` | Reboot |
| `systemctl poweroff` | Power off |
| `systemctl suspend` | Suspend to RAM |
| `systemctl hibernate` | Hibernate |
| `systemctl daemon-reload` | Reload unit files |

## Troubleshooting

| Command | Description |
|---------|-------------|
| `systemctl show svc` | All properties |
| `systemctl cat svc` | Show unit file |
| `systemctl edit svc` | Edit override |
| `systemctl reset-failed svc` | Clear failed state |

## Related Notes

- [[SystemdAndInit]] — systemd concepts
- [[ServiceManagement]] — Service workflow
- [[systemctl]] — systemctl command
