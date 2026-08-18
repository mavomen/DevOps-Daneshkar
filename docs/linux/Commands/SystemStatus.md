---
id: SystemStatus
aliases: []
tags: []
---

# System Status

Checking system health during security incident response.

## uptime

Shows how long the system has been running and current load.

```bash
uptime
# 00:40:18 up 3 days, 20:36, 1 user, load average: 1.02, 0.81, 0.75
```

### Format

```
current_time up up_time, users_logged_in, load average: 1min, 5min, 15min
```

### Load Average Interpretation

| Load | Cores | CPU Usage |
|------|-------|-----------|
| 1.00 | 1 core | 100% busy |
| 1.00 | 4 cores | 25% busy |
| 1.00 | 8 cores | 12.5% busy |

> [!NOTE]
> Decreasing load (1.02 → 0.81 → 0.75) means the system is calming down after a busy period.

## free

Shows RAM and swap usage.

```bash
free
```

### Example Output

| Column | Value | Meaning |
|--------|-------|---------|
| `total` | 16,233,212 | 15.5 GB physical RAM |
| `used` | 5,236,212 | 5.0 GB actively used |
| `free` | 890,284 | 0.85 GB completely empty |
| `buff/cache` | 11,125,260 | 10.6 GB file cache (reclaimable) |
| `available` | 10,997,000 | **10.5 GB available for new apps** |

> [!NOTE]
> Don't panic about low `free` — Linux uses cache for performance. `available` is the real free memory.

### Swap

| Column | Value | Meaning |
|--------|-------|---------|
| `total` | 4,194,300 | 4 GB swap partition |
| `used` | 720,676 | 0.7 GB in use |
| `free` | 3,473,624 | 3.3 GB available |

> [!NOTE]
> Some swap usage is normal — Linux swaps out idle processes to free RAM for cache.

## Quick Health Commands

```bash
# Running processes
ps aux --sort=-%mem | head -20              # Top memory consumers
ps aux --sort=-%cpu | head -20              # Top CPU consumers

# Disk usage
df -h                                       # Filesystem usage
du -sh /var/log/*                           # Log directory sizes

# Network connections
ss -tlnp                                    # Listening ports
ss -tnp                                     # Active connections
```

## Related Notes

- [[UserAccountInvestigation]] — User accounts
- [[AuthenticationLogs]] — Auth logs
- [[03-SecurityMOC]] — Linux Security MOC
