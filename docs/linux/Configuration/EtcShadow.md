---
id: EtcShadow
aliases: []
tags: []
---

# /etc/shadow — Password Hash & Policy

Encrypted passwords and password aging policies. Requires root to read.

## Format

```
username:password_hash:last_change:min:max:warn:inactive:expire:reserved
```

| Field | Meaning |
|-------|---------|
| `password_hash` | Encrypted password (`!`/`*` = locked) |
| `last_change` | Days since Jan 1, 1970 |
| `min` | Minimum days between changes |
| `max` | Maximum password age |
| `warn` | Warning period before expiry |
| `inactive` | Days after expiry before lock |
| `expire` | Absolute expiry date |

## Hash Types

| Prefix | Algorithm | Strength |
|--------|-----------|----------|
| `$1$` | MD5 | Weak |
| `$5$` | SHA-256 | Strong |
| `$6$` | SHA-512 | Strongest |
| `!` or `*` | Locked | No login |

## Security Commands

```bash
sudo cat /etc/shadow                        # View (root only)
passwd -S username                          # Password status
sudo chage -l username                      # Password aging info
sudo chage -M 90 username                   # Force 90-day expiry
```

## Related Notes

- [[EtcPasswd]] — User account info
- [[PasswordAndShadow]] — Password investigation
- [[UserAccountInvestigation]] — Investigation workflow
