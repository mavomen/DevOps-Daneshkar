---
id: 06-BestPracticesMOC
aliases: []
tags: []
---

# Linux Best Practices — MOC

Security, organization, and operational excellence.

## Security

- [[SecurityHardening]] — System hardening checklist
- [[FirewallRules]] — Firewall configuration

## Organization

- [[FileOrganization]] — Directory structure and naming
- [[BackupStrategies]] — Backup approaches

## Operations

- [[SystemUpdates]] — Safe update procedures
- [[UserProvisioning]] — User account workflows
- [[LogRotation]] — Log management
- [[ServiceManagement]] — systemd service lifecycle
- [[BackupAndRestore]] — Backup and recovery

## Development

- [[ScriptingStandards]] — Shell scripting best practices

## Performance

- [[PerformanceTuning]] — System optimization

## Quick Reference

```bash
# Security hardening
sudo ufw status                             # Firewall status
sudo auditctl -l                            # Audit rules
sshd -t                                     # SSH config test

# System updates
apt update && apt upgrade -y

# Backup
rsync -avz --delete /home/ /backup/home/    # Quick backup

# Performance
top -bn1 | head -20                         # CPU/memory
iostat -xz 1 3                              # Disk I/O
ss -s                                       # Network stats
```

## Related Notes

- [[00-Linux]] — Main Linux MOC
- [[04-ConfigurationMOC]] — Config files
