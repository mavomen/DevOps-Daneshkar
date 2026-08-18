---
id: 00-LinuxSecurityMOC
aliases: []
tags: []
---

# Linux Security — MOC

Investigating and responding to security incidents on Linux systems.

## Investigation Areas

### User Accounts
- [[UserAccountInvestigation]] — /etc/passwd, passwd -S, find -nouser
- [[PasswordAndShadow]] — /etc/shadow, password hashes
- [[GroupInvestigation]] — /etc/group, group membership

### Authentication & Access
- [[SudoConfiguration]] — /etc/sudoers, sudo rules
- [[LoginTracking]] — lastlog2, login history
- [[AuthenticationLogs]] — journalctl, auth logs

### System Health
- [[SystemStatus]] — uptime, free, load averages

### Tools
- [[GrepRegexPatterns]] — grep regex patterns

## Configuration Files

- [[EtcPasswd]] — User account database
- [[EtcShadow]] — Password hashes and aging
- [[EtcGroup]] — Group database
- [[EtcSudoers]] — Sudo access rules
- [[SshdConfig]] — SSH server hardening
- [[EtcEnvironment]] — Environment variables

## Security Best Practices

- [[SecurityHardening]] — Hardening checklist
- [[FirewallRules]] — Firewall configuration

## Troubleshooting

- [[PermissionDenied]] — Permission issues
- [[NetworkIssues]] — Network diagnostics
- [[BootFailures]] — Boot recovery
- [[RecoveryModes]] — Recovery boot options

## Quick Reference

```bash
# User investigation
cat /etc/passwd                             # All users
grep :0: /etc/passwd                        # UID 0 accounts
passwd -S <user>                            # Password status
sudo find / -nouser -print                  # Orphaned files

# Group investigation
cat /etc/group                              # All groups
groups <user>                               # User's groups
id <user>                                   # Full identity

# Access investigation
sudo cat /etc/sudoers                       # Sudo rules
sudo -l                                     # Your sudo access

# Login tracking
lastlog2                                    # Last logins
last                                        # Login history

# Auth logs
sudo journalctl -g "Failed password" -b     # Failed attempts
sudo journalctl -g "sudo" -b                # Sudo usage

# System status
uptime                                      # Load and uptime
free                                        # Memory usage
ps aux --sort=-%mem | head                  # Top processes
```

## Related Notes

- [[00-Linux]] — Main Linux MOC
