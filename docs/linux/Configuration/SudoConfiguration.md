---
id: SudoConfiguration
aliases: []
tags: []
---

# Sudo Configuration

Investigating sudo rules for security incident response.

## /etc/sudoers

Defines who can run what as root. Must be edited with `visudo`.

```bash
sudo cat /etc/sudoers
```

### Key Rules

| Rule | Meaning |
|------|---------|
| `root ALL=(ALL:ALL) ALL` | Root can do anything |
| `%wheel ALL=(ALL:ALL) ALL` | Wheel group members can sudo |
| `# %wheel ALL=(ALL:ALL) NOPASSWD: ALL` | Commented — password required |
| `@includedir /etc/sudoers.d` | Load extra rules from directory |

### Security Defaults

| Setting | Purpose |
|---------|---------|
| `Defaults secure_path` | Restricts PATH for sudo commands |
| `Defaults env_keep` | Preserves editor settings for visudo |
| `Defaults !use_pty` | Disables pseudo-terminal (optional) |

## What This Means for Your User

1. **Full admin rights** — can run any command as any user
2. **Password required** — must authenticate each time
3. **Safe PATH** — sudo ignores personal PATH, uses system paths

## Quick Checks

```bash
# Check who can sudo
sudo grep -v '^#' /etc/sudoers | grep -v '^$'

# Check sudoers.d directory
ls -la /etc/sudoers.d/

# Test your sudo access
sudo -l
```

## Related Notes

- [[GroupInvestigation]] — Group membership (wheel group)
- [[PasswordAndShadow]] — Password files
- [[03-SecurityMOC]] — Linux Security MOC
