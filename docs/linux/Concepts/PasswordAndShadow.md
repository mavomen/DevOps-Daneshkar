---
id: PasswordAndShadow
aliases: []
tags: []
---

# Password & Shadow Investigation

Investigating password files for security incident response.

## /etc/shadow

Contains encrypted password hashes and password policy details.

```bash
sudo cat /etc/shadow
```

### Format

```
username:password_hash:last_change:min:max:warn:inactive:expire:reserved
```

### Key Indicators

| Hash | Meaning |
|------|---------|
| `!` or `*` | Locked account, no password |
| `$6$...` | SHA-512 hash (strong) |
| `$5$...` | SHA-256 hash |
| `$1$...` | MD5 hash (weak) |
| Empty | No password required |

### Example

```
root:$6$...:19000:0:99999:7:::
mava:$6$...:19000:0:99999:7:::
bin:*:20627:::::
```

> [!WARNING]
> Never share actual hash strings. They are what attackers try to crack.

## Security Checks

```bash
# Check if any non-root users have UID 0
grep ':0:0:' /etc/passwd

# Find accounts with no password
sudo awk -F: '($2 == "" || $2 == "!") {print $1}' /etc/shadow

# Check password age
sudo chage -l mava
```

## Related Notes

- [[UserAccountInvestigation]] — User account details
- [[SudoConfiguration]] — Sudo configuration
- [[03-SecurityMOC]] — Linux Security MOC
