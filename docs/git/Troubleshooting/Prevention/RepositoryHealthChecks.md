---
id: RepositoryHealthChecks
aliases: []
tags: []
---

# Repository Health Checks

Periodic checks to detect issues early (corruption, bloat, stale refs).

## Integrity checks

```bash
git fsck --full
```

## Object / size overview

```bash
git count-objects -v
du -sh .git
```

## Remote tracking cleanup

```bash
git fetch --prune
```

## Working tree cleanup (untracked junk)

Preview first:

```bash
git clean -nd
```

Then clean:

```bash
git clean -fd
```

## Related Notes

- [[CorruptedRepository]]
- [[LargeFileIssues]]
- [[SlowGitOperations]]
