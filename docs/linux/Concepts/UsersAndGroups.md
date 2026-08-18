---
id: UsersAndGroups
aliases: []
tags: []
---

# Users & Groups

Managing user accounts and group membership.

## Key Files

| File | Purpose |
|------|---------|
| `/etc/passwd` | User accounts (username:UID:GID:home:shell) |
| `/etc/shadow` | Password hashes and policies |
| `/etc/group` | Groups and membership |

## User Commands

```bash
id username                                 # UID, GID, groups
whoami                                      # Current user
groups username                             # User's groups
```

## Create/Modify/Delete

```bash
useradd -m -s /bin/bash newuser             # Create user with home
passwd newuser                              # Set password
usermod -aG docker newuser                  # Add to group
usermod -s /bin/zsh newuser                 # Change shell
userdel newuser                             # Delete user
userdel -r newuser                          # Delete with home dir
```

## Group Commands

```bash
groupadd developers                         # Create group
groupdel developers                         # Delete group
usermod -aG developers alice                # Add user to group
gpasswd -d alice developers                 # Remove from group
```

## Key Groups

| Group | Purpose |
|-------|---------|
| `wheel` / `sudo` | Admin (sudo access) |
| `docker` | Docker access (effectively root) |
| `www-data` | Web server files |
| `users` | General users |

## Related Notes

- [[UserAccountInvestigation]] — Investigating accounts
- [[GroupInvestigation]] — Group investigation
- [[SudoConfiguration]] — Sudo configuration
- [[useradd]] — useradd command
