---
id: git-fsck
aliases: []
tags: []
---

# git fsck

Verify the connectivity and validity of objects in the Git object database.

## Syntax

```bash
git fsck
git fsck --full
```

## Description

`git fsck` checks repository integrity and reports missing/corrupt objects.

## Common usage

### Full integrity check

```bash
git fsck --full
```

## When to use

- after disk issues / crashes
- when Git reports corrupt objects
- when operations fail unexpectedly and you suspect repo corruption

## What to do if fsck reports corruption

- If you have a good remote: reclone (often simplest).
- If only local exists: treat as recovery/forensics; results vary.

See: [[Troubleshooting/CommonProblems/CorruptedRepository|Corrupted Repository]]

## Related Notes

- [[Repository]]
- [[Troubleshooting/CommonProblems/CorruptedRepository|Corrupted Repository]]
