---
id: EtcPasswd
aliases: []
tags: []
---

# /etc/passwd — User Account Database

Each line defines one user account.

## Format

```
username:password:UID:GID:GECOS:home_directory:login_shell
```

| Field | Meaning |
|-------|---------|
| `username` | Login name |
| `password` | `x` = shadow password, `!`/`*` = locked |
| `UID` | User ID (0=root, 1000+=regular users) |
| `GID` | Primary group ID |
| `GECOS` | Full name, contact info |
| `home` | Home directory path |
| `shell` | Login shell (`/sbin/nologin` = no login) |

## Key Users

| User | UID | Shell | Purpose |
|------|-----|-------|---------|
| `root` | 0 | bash | Superuser |
| `nobody` | 65534 | nologin | Lowest privilege |
| `www-data` | 33 | nologin | Web server |
| `systemd-network` | 100+ | nologin | Network management |

## Security Checks

```bash
grep ':0:0:' /etc/passwd                    # Only root should have UID 0
awk -F: '$7 != "/sbin/nologin" && $7 != "/usr/bin/nologin" {print}' /etc/passwd  # Users with login shells
```

## Related Notes

- [[PasswordAndShadow]] — /etc/shadow
- [[GroupInvestigation]] — /etc/group
- [[UserAccountInvestigation]] — Investigation workflow
- [[UsersAndGroups]] — User management
