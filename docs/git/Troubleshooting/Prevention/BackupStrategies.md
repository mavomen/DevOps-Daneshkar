---
id: BackupStrategies
aliases: []
tags: []
---

# Backup Strategies

Git is distributed, but you still need deliberate backup habits.

## Practical backups

- push important branches to a remote (origin/upstream)
- push tags for releases
- ensure at least one additional clone exists for critical repos

## Minimal backup routine

```bash
git push --all
git push --tags
```

## Offsite backups

- host on GitHub/GitLab or internal Git server
- mirror to a second remote if needed

## Before risky operations

Create a backup branch:

```bash
git branch backup/$(date +%Y-%m-%d)-before-risk
```

Or push feature branch before rewriting:

```bash
git push -u origin <branch>
```

## Related Notes

- [[git-push]]
- [[git-tag]]
- [[SafeGitPractices]]
