---
id: 05-TroubleshootingMOC
aliases: []
tags: []
---

# Linux Troubleshooting — MOC

Common issues and diagnostic procedures.

## Boot & System

- [[BootFailures]] — Boot problems and recovery
- [[RecoveryModes]] — GRUB recovery options
- [[ServiceFailed]] — Failed systemd services

## Filesystem & Disk

- [[DiskFull]] — Disk space issues
- [[PermissionDenied]] — Permission problems

## Processes

- [[ProcessAnalysis]] — Process investigation

## Networking

- [[NetworkIssues]] — Network connectivity

## Logs

- [[LogAnalysis]] — Log searching and analysis

## Quick Reference

```bash
# Boot issues
journalctl -b                               # Current boot
dmesg | tail -50                             # Kernel messages
systemctl --failed                           # Failed services

# Disk space
df -h                                       # Disk usage
du -sh /* 2>/dev/null | sort -hr | head    # Largest dirs
find / -type f -size +100M -ls 2>/dev/null # Large files

# Permissions
ls -la file                                 # Check permissions
namei -l /path/to/file                      # Path permissions
id user                                     # User groups

# Network
ip addr show                                # IP addresses
ss -tlnp                                    # Listening ports
dig example.com                             # DNS test

# Logs
journalctl -u service -f                    # Follow logs
grep -i error /var/log/syslog               # Search errors
```

## Related Notes

- [[00-Linux]] — Main Linux MOC
- [[03-SecurityMOC]] — Security investigation
