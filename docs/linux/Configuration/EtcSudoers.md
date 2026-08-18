---
id: EtcSudoers
aliases: []
tags: []
---

# /etc/sudoers — Sudo Configuration

Defines which users can run commands as root. Edit only with `visudo`.

## Format

```
user    host=(runas)  commands
```

## Example Rules

```
root    ALL=(ALL:ALL)  ALL                   # Root can do anything
%wheel  ALL=(ALL:ALL)  ALL                   # Wheel group: full sudo
alice   ALL=(ALL)      /usr/bin/systemctl    # Alice: only systemctl
bob     ALL=(ALL)       NOPASSWD: /usr/bin/docker  # Bob: docker, no password
```

## Security Defaults

| Setting | Purpose |
|---------|---------|
| `Defaults secure_path` | Safe PATH for sudo commands |
| `Defaults env_keep` | Preserve env vars for visudo |
| `Defaults timestamp_timeout` | Sudo cache time (default 5 min) |

## Key Commands

```bash
sudo visudo                                 # Edit safely
sudo visudo -f /etc/sudoers.d/custom        # Edit drop-in file
sudo -l                                     # Your sudo privileges
sudo -u postgres psql                       # Run as specific user
```

## Drop-in Files

```bash
# /etc/sudoers.d/myapp — cleaner than editing main file
cat > /etc/sudoers.d/myapp << 'EOF'
deploy ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart myapp
EOF
chmod 440 /etc/sudoers.d/myapp
```

## Related Notes

- [[SudoConfiguration]] — Sudo investigation
- [[UsersAndGroups]] — User management
- [[SecurityHardening]] — Security best practices
