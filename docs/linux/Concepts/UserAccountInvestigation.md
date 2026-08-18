---
id: UserAccountInvestigation
aliases: []
tags: []
---

# User Account Investigation

Investigating user accounts for security incident response.

## /etc/passwd

The user account database. Each line represents one user.

```bash
cat /etc/passwd
```

### Format

```
username:password:UID:GID:GECOS:home_directory:login_shell
```

### Example Entries

| Username | UID | Shell | What It Is |
|----------|-----|-------|------------|
| `root` | 0 | `/usr/bin/bash` | Superuser, full control |
| `bin` | 1 | `/usr/bin/nologin` | Legacy system user |
| `daemon` | 2 | `/usr/bin/nologin` | Background services |
| `http` | 33 | `/usr/bin/nologin` | Web server (Apache/Nginx) |
| `nobody` | 65534 | `/usr/bin/nologin` | Lowest-privilege user |
| `mava` | 1000 | `/bin/zsh` | Personal user account |
| `git` | 966 | `/usr/bin/git-shell` | Git daemon (restricted) |
| `postgres` | 963 | `/usr/bin/bash` | PostgreSQL database |

> [!NOTE]
> Only `root`, `mava`, and `postgres` have real login shells. All others are system/service accounts.

## passwd -S

Check password status for a user.

```bash
passwd -S mava
# mava P 2026-06-23 0 99999 7 -1
```

### Output Format

| Field | Meaning |
|-------|---------|
| `P` | Usable password set |
| `L` | Account locked |
| `NP` | No password |
| `2026-06-23` | Last password change |
| `0` | Minimum days (can change anytime) |
| `99999` | Maximum days (~never expires) |
| `7` | Warning period (days) |
| `-1` | No inactivity timer |

## grep :0: — Find UID 0 Accounts

```bash
grep :0: /etc/passwd
# root:x:0:0::/root:/usr/bin/bash
```

Only `root` should have UID 0. Any other entry is a red flag.

## find / -nouser — Find Orphaned Files

```bash
sudo find / -nouser -print
```

Scans entire filesystem for files owned by UIDs that don't exist in `/etc/passwd`.

### Common Results (Ignore)

| Result | Reason |
|--------|--------|
| `/proc/*` errors | Virtual filesystem, processes ended mid-scan |
| `/run/user/1000/gvfs` | FUSE mount, restricted by mount type |
| `/var/lib/containerd/*` | Container overlay layers (harmless) |

### Actionable Results

| Result | Action |
|--------|--------|
| ISO files, personal data | `sudo chown -R mava:mava /path/` |
| Container debris | `docker system prune` (don't delete manually) |

## Related Notes

- [[PasswordAndShadow]] — Password file investigation
- [[GroupInvestigation]] — Group membership
- [[GrepRegexPatterns]] — grep patterns
- [[03-SecurityMOC]] — Linux Security MOC
