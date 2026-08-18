---
id: Crontab
aliases: []
tags: []
---

# Crontab — Scheduled Task Configuration

Automates recurring tasks via the cron daemon.

## Crontab Format

```
┌───────── minute (0-59)
│ ┌───────── hour (0-23)
│ │ ┌───────── day of month (1-31)
│ │ │ ┌───────── month (1-12)
│ │ │ │ ┌───────── day of week (0-7, 0=7=Sun)
│ │ │ │ │
* * * * *  command
```

## Examples

```bash
0 2 * * *   /usr/local/bin/backup.sh       # Daily at 2 AM
*/5 * * * * /usr/bin/check-health.sh        # Every 5 minutes
0 9 * * 1   /usr/bin/weekly-report.sh       # Monday at 9 AM
30 18 * * 1-5 /usr/bin/weekday-task.sh      # Weekdays at 6:30 PM
0 0 1 * *   /usr/bin/monthly-cleanup.sh     # First of month
```

## Crontab Commands

```bash
crontab -l                                 # List your cron jobs
crontab -e                                 # Edit your crontab
crontab -r                                 # Remove all cron jobs
sudo crontab -u alice -l                   # View user's crontab
```

## Special Strings

| String | Equivalent |
|--------|------------|
| `@reboot` | At system startup |
| `@daily` | `0 0 * * *` |
| `@weekly` | `0 0 * * 0` |
| `@monthly` | `0 0 1 * *` |
| `@yearly` | `0 0 1 1 *` |

## Related Notes

- [[LogSystem]] — Cron logs at /var/log/cron
- [[SystemdAndInit]] — systemd timers as alternative
- [[Crontab]] — Scheduled tasks
