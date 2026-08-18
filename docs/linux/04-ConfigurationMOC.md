---
id: 04-ConfigurationMOC
aliases: []
tags: []
---

# Linux Configuration — MOC

System configuration files and management.

## User & Group Files

- [[EtcPasswd]] — User account database
- [[EtcShadow]] — Password hashes and aging
- [[EtcGroup]] — Group database

## Access Control

- [[EtcSudoers]] — Sudo access rules
- [[SudoConfiguration]] — Sudo investigation
- [[SshdConfig]] — SSH server configuration

## Filesystem & Boot

- [[EtcFstab]] — Mount table

## Environment

- [[EtcEnvironment]] — System-wide environment variables

## Scheduled Tasks

- [[Crontab]] — Cron job configuration

## Quick Reference

```bash
# User/group files
cat /etc/passwd                             # All users
cat /etc/shadow                             # Password hashes (root only)
cat /etc/group                              # All groups

# Access
cat /etc/sudoers                            # Sudo rules (use visudo)
sudo visudo                                 # Safe edit

# SSH
sudo sshd -t                                # Test config
sudo systemctl reload sshd                  # Apply changes

# Mounts
cat /etc/fstab                              # Mount table
mount -a                                    # Mount all from fstab

# Cron
crontab -l                                  # List cron jobs
crontab -e                                  # Edit cron jobs
```

## Related Notes

- [[00-Linux]] — Main Linux MOC
- [[03-SecurityMOC]] — Security
