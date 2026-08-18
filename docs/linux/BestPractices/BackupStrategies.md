---
id: BackupStrategies
aliases: []
tags: []
---

# Backup Strategies — Best Practices

Approaches and tools for data protection.

## Backup Types

| Type | Description | Speed | Recovery |
|------|-------------|-------|----------|
| **Full** | Complete copy of all data | Slow | Fast |
| **Incremental** | Only changes since last backup | Fast | Slower |
| **Differential** | Changes since last full backup | Medium | Medium |

## What to Backup

- `/etc/` — Configuration files
- `/home/` — User data
- `/var/lib/` — Application data
- Database dumps (if applicable)
- Cron jobs and service configs
- SSH keys and certificates

## Tools

```bash
# rsync — incremental sync
rsync -avz --delete /home/ /backup/home/
rsync -avz -e ssh /home/ user@remote:/backup/

# tar — create archives
tar -czf backup-$(date +%Y%m%d).tar.gz /etc/ /home/

# restic — modern, encrypted backups
restic -r /backup init
restic -r /backup backup /home
restic -r /backup snapshots
```

## Automated Backup Script

```bash
#!/bin/bash
BACKUP_SRC="/home /etc"
BACKUP_DST="/backup/$(date +%Y%m%d)"
LOG="/var/log/backup.log"

for src in $BACKUP_SRC; do
    rsync -avz "$src" "$BACKUP_DST/" 2>&1 | tee -a "$LOG"
done

# Clean backups older than 30 days
find /backup/ -maxdepth 1 -mtime +30 -exec rm -rf {} \;
```

## Related Notes

- [[DiskManagement]] — Storage management
- [[FileOrganization]] — Directory structure
- [[BackupAndRestore]] — Restore procedures
- [[SystemUpdates]] — Update workflows
