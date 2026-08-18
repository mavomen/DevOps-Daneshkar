---
id: LoginTracking
aliases: []
tags: []
---

# Login Tracking

Tracking user login history for security incident response.

## lastlog2

Shows the most recent login time for every user.

```bash
lastlog2
```

### Example Output

| Username | Port | From | Latest |
|----------|------|------|--------|
| `mava` | `tty1` | _(local)_ | Sat Jul 25 04:04:22 2026 |
| `root` | `tty1` | _(local)_ | Wed Jun 24 02:59:28 2026 |

### Fields

| Field | Meaning |
|-------|---------|
| `tty1` | Physical console (not SSH) |
| Blank "From" | Local login (not remote) |
| Timestamp | Exact last login time |

> [!NOTE]
> System/service accounts (bin, daemon, http, etc.) never appear because they have `nologin` shells.

## last / lastb

```bash
last                                        # Successful logins
lastb                                       # Failed logins (needs sudo)
last -n 10                                  # Last 10 entries
last mava                                   # Logins for specific user
```

## Related Notes

- [[AuthenticationLogs]] — Detailed auth logs
- [[UserAccountInvestigation]] — User accounts
- [[03-SecurityMOC]] — Linux Security MOC
