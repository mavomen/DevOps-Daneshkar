---
id: SlowGitOperations
aliases: []
tags: []
---

# Slow Git Operations

When commands like `status`, `log`, `fetch`, or `checkout` become slow.

## Common causes

- huge repo / many files
- large untracked directories
- large `.git` history
- slow filesystem (network mounts)
- huge diffs / rename detection

## Diagnosis

```bash
git status -sb
git count-objects -v
```

Check untracked bloat:

```bash
git clean -nd
```

## Quick improvements

- prune stale remote branches:

```bash
git fetch --prune
```

- delete untracked build artifacts:

```bash
git clean -fd
```

- avoid massive untracked dirs inside repo (move build output elsewhere)

## Structural improvements

- stop committing generated artifacts
- remove large files from history if needed
- consider repo splitting or better monorepo tooling

## Related Notes

- [[PerformanceOptimization]]
- [[LargeRepositoryHandling]]
- [[git-clean]]
- [[git-fetch]]
