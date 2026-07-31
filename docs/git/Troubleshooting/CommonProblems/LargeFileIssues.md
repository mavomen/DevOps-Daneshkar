---
id: LargeFileIssues
aliases: []
tags: []
---

# Large File Issues

Problems caused by large binaries or oversized history.

## Symptoms

- `git push` rejected due to file size limits
- repository becomes slow to clone/fetch
- CI checkout time explodes

## Diagnosis

- identify large files in working tree:

```bash
du -sh .
du -sh .git
```

- check what’s untracked junk:

```bash
git status
git clean -nd
```

## Quick Fixes

### If a large file is untracked

Add to `.gitignore`, then remove it from disk if needed.

### If a large file was committed but not pushed yet

Undo the commit locally:

```bash
git reset --soft HEAD~1
git restore --staged <large-file>
# optionally delete it
rm <large-file>
git commit -m "commit without large file"
```

### If pushed (history already contains it)

You need history rewrite (coordinated):

- [[git-filter-branch]]
- rotate secrets if applicable

## Prevention

- enforce `.gitignore` rules
- use artifact storage or LFS if team policy allows
- add hooks/CI checks to block oversized additions

## Related Notes

- [[LargeRepositoryHandling]]
- [[GitIgnorePatterns]]
- [[git-clean]]
- [[git-filter-branch]]
