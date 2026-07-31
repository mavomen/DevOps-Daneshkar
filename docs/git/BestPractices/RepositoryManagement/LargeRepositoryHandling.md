---
id: LargeRepositoryHandling
aliases: []
tags: []
---

# Large Repository Handling

Large repos create pain in cloning, fetching, CI, and developer experience. This note collects practical mitigations.

## Symptoms of a large repo

- slow `git clone`
- slow `git fetch` / `git status`
- huge CI checkout times
- large binary assets inside Git history

Related:

- [[git-fetch]]
- [[git-clone]]
- [[git-clean]]
- [[git-filter-branch]]
- [[GitObjects]]

## Primary causes (common)

- large binaries committed directly
- generated artifacts committed repeatedly
- monorepo scaling without tooling
- overly deep history needed by CI for every job

## Mitigations (practical)

### 1) Keep binaries out of Git history (preferred)

- store binaries in artifact storage
- consider Git LFS if your org uses it (policy-based)

### 2) Don’t commit generated artifacts (unless required)

- add to `.gitignore` (see [[GitIgnorePatterns]])
- generate in CI instead

### 3) Prune what you don’t need

- remove stale remote refs:

```bash
git fetch --prune
```

- clean untracked build output:

```bash
git clean -fd
```

### 4) Avoid repeated massive history rewrites

If you must remove files from history, use careful, coordinated rewriting (see [[git-filter-branch]]) and rotate secrets if relevant.

### 5) CI checkout strategy

- shallow clones can speed up jobs, but be careful if you need tags/history
- fetch tags only when release jobs need them

See: [[CiCdIntegration]]

## Team policy recommendations

- define what is allowed in Git history (size limits, file types)
- enforce via hooks + CI:
  - pre-commit/pre-push checks (see [[GitHooks]])

## Related notes

- [[BestPractices/RepositoryManagement/PerformanceOptimization|Performance Optimization]]
- [[BestPractices/RepositoryManagement/SecurityPractices|Security Practices]]
