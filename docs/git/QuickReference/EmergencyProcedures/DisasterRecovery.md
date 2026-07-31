---
id: DisasterRecovery
aliases: []
tags: []
---

# Disaster Recovery

Worst-case situations: repo corruption, history rewrite accidents, secrets pushed, or remote mishaps.

## Scenario A: You force-pushed the wrong history

1. Stop pushing further.
2. Use reflog to find the previous state:

```bash
git reflog
```

3. Create a rescue branch:

```bash
git branch rescue/pre-force HEAD@{n}
```

4. Coordinate with team, then restore remote safely:

```bash
git push --force-with-lease origin rescue/pre-force:main
```

## Scenario B: Secrets were committed and pushed

1. Rotate/revoke the secrets immediately.
2. Remove from history if required (coordinated rewrite):
   - see [[git-filter-branch]]
3. Notify maintainers, document incident.

## Scenario C: Local repo corrupted

Preferred fix: re-clone.

```bash
cd ..
mv repo repo.broken
git clone <url>
```

If no remote exists and only local is damaged:

```bash
git fsck --full
git reflog --all
```

## Scenario D: Remote deleted / unavailable

- If any developer has a complete clone, you can restore by pushing to a new remote.
- Ensure tags and all branches are pushed:

```bash
git push --all
git push --tags
```

## Related Notes

- [[git-reflog]]
- [[git-filter-branch]]
- [[Troubleshooting/CommonProblems/CorruptedRepository|CorruptedRepository]]
- [[BestPractices/RepositoryManagement/SecurityPractices|SecurityPractices]]
