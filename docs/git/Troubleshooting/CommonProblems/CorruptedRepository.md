---
id: CorruptedRepository
aliases: []
tags: []
---

# Corrupted Repository

Repository corruption means Git objects/refs are missing or inconsistent.

## Symptoms

- errors like “fatal: loose object … is corrupt”
- operations fail unexpectedly (`checkout`, `log`, `fsck`)
- missing objects during fetch/checkout

## First Response (recommended)

Reclone if possible:

```bash
cd ..
mv repo repo.broken
git clone <url>
```

## Diagnosis (if you must)

```bash
git fsck --full
```

## Recovery options

- If you have a good remote: reclone (best).
- If remote is also bad:
  - find another clone (teammate) and re-publish it.

## If only local exists

- you may recover some objects via `git fsck --lost-found`
- success varies; treat it like data forensics.

## Prevention

- avoid manual edits inside `.git/`
- use stable storage and backups
- keep remotes (every clone is a backup in DVCS)

## Related Notes

- [[EmergencyRecovery]]
- [[BackupStrategies]]
