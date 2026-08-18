---
id: EtcGroup
aliases: []
tags: []
---

# /etc/group — Group Database

Defines all groups and their members.

## Format

```
group_name:password:GID:member_list
```

| Field | Meaning |
|-------|---------|
| `password` | `x` = shadow group (rarely used) |
| `GID` | Group ID |
| `member_list` | Comma-separated supplementary members |

## Important Groups

| Group | GID | Purpose |
|-------|-----|---------|
| `root` | 0 | System admin |
| `wheel` / `sudo` | varies | Admin (sudo access) |
| `docker` | varies | Docker access |
| `www-data` | 33 | Web server |
| `users` | 100 | General users |

## View Group Info

```bash
cat /etc/group                              # All groups
groups username                             # User's groups
id -nG username                             # Group names only
getent group docker                         # Specific group members
```

## Manage Groups

```bash
groupadd devteam                            # Create group
gpasswd -a alice devteam                    # Add user to group
gpasswd -d alice devteam                    # Remove from group
groupdel devteam                            # Delete group
```

## Related Notes

- [[EtcPasswd]] — User accounts
- [[GroupInvestigation]] — Group investigation
- [[UsersAndGroups]] — User/group management
