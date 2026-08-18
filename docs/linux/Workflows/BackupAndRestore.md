---
id: BackupAndRestore
aliases: []
tags: []
---

# Backup and Restore — Workflow

Practical backup and disaster recovery procedures.

## Backup Checklist

- [ ] Identify critical data (`/etc/`, `/home/`, app data)
- [ ] Choose backup tool (rsync, restic, borg)
- [ ] Set backup schedule
- [ ] Test restore procedure
- [ ] Verify backup integrity

## Quick Backup with rsync

```bash
# Full backup
rsync -avz --delete \
    --exclude='*.log' \
    --exclude='.cache' \
    /home/ /backup/home/$(date +%Y%m%d)/

# Incremental (only changes)
rsync -avz /home/ /backup/home/latest/
```

## Restore Procedure

```bash
# List available backups
ls -la /backup/home/

# Restore specific files
rsync -avz /backup/home/latest/alice/ /home/alice/

# Full restore
rsync -avz /backup/home/latest/ /home/
```

## Database Backup

```bash
# PostgreSQL
pg_dump -U postgres mydb > /backup/mydb.sql
pg_restore -U postgres mydb < /backup/mydb.sql

# MySQL
mysqldump -u root -p mydb > /backup/mydb.sql
mysql -u root -p mydb < /backup/mydb.sql
```

## Verify Backup

```bash
# Test archive integrity
tar -tzf backup.tar.gz > /dev/null

# Test rsync dry-run
rsync -avzn /backup/home/ /home/ | head -20
```

## Related Notes

- [[BackupStrategies]] — Strategy overview
- [[DiskManagement]] — Storage
- [[SystemUpdates]] — Backup before updates
