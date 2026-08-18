---
id: AuthenticationLogs
aliases: []
tags: []
---

# Authentication Logs

Analyzing authentication logs for security incident response.

## journalctl (Arch/systemd)

On Arch Linux, auth logs are in the systemd journal, not `/var/log/auth.log`.

```bash
# All authentication events this boot
sudo journalctl -g "pam|sudo|sshd|login" -b

# Just sudo commands
sudo journalctl -g "sudo" -b

# Failed login attempts
sudo journalctl -g "Failed password" -b

# Login sessions
sudo journalctl -g "session opened|login" -b

# Follow real-time (like tail -f)
sudo journalctl -b -f
```

## Debian/Ubuntu (auth.log)

```bash
# Recent auth events
sudo tail -50 /var/log/auth.log

# Failed SSH attempts
sudo grep "Failed password" /var/log/auth.log

# Successful logins
sudo grep "Accepted" /var/log/auth.log

# Sudo usage
sudo grep "sudo" /var/log/auth.log
```

## What to Look For

| Pattern | Meaning |
|---------|---------|
| `Failed password` | Brute force attempt |
| `Accepted publickey` | SSH key login |
| `session opened` | User session started |
| `sudo: root : TTY=` | Sudo command executed |
| `pam_unix(su:auth)` | Switch user attempt |

## Related Notes

- [[LoginTracking]] — Login history
- [[UserAccountInvestigation]] — User accounts
- [[03-SecurityMOC]] — Linux Security MOC
