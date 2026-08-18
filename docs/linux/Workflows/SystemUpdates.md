---
id: SystemUpdates
aliases: []
tags: []
---

# System Updates — Workflow

Safe procedure for updating Linux systems.

## Before Updating

```bash
# Check current state
cat /etc/os-release
uname -r
uptime
df -h
free -h

# Check for available updates
apt list --upgradable                       # Ubuntu/Debian
```

## Update Procedure

```bash
sudo apt update && sudo apt upgrade -y
sudo apt autoremove -y
sudo apt clean
```

## Post-Update

```bash
# Check for services needing restart
sudo apt install -y debian-goodies
sudo checkrestart                           # Services needing restart

# Reboot if kernel updated
[[ $(uname -r) != $(ls /boot/vmlinuz-* | sort -V | tail -1 | xargs basename | sed 's/vmlinuz-//') ]] && sudo reboot

# Verify critical services
systemctl status nginx postgresql docker
```

## Rollback

```bash
sudo apt install pkg=version                # Install specific version
```

## Related Notes

- [[PackageManagement]] — Package managers
- [[LogSystem]] — Check logs after update
- [[BackupStrategies]] — Backup before update
- [[RecoveryModes]] — Recovery if broken
