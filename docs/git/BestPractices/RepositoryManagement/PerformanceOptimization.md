---
id: PerformanceOptimization
aliases: []
tags: []
---

# Performance Optimization

Practical ways to keep Git operations fast for developers and CI.

## What gets slow

- `git status` in huge working trees
- `git clone` / `git fetch` in large repos
- merges/rebases with frequent conflicts
- CI checkout and dependency steps

Related:

- [[git-fetch]]
- [[git-clone]]
- [[git-clean]]
- [[BestPractices/RepositoryManagement/LargeRepositoryHandling|Large Repository Handling]]

## Developer-side tips

### Keep your working tree clean

- delete build junk:

```bash
git clean -fd
```

- avoid keeping huge untracked directories around

### Prune stale remote refs

```bash
git fetch --prune
```

### Prefer fetch + inspect + integrate

Instead of blindly pulling:

```bash
git fetch origin
git log --oneline --decorate --graph --all --max-count=30
# then merge/rebase intentionally
```

See: [[Workflows/DailySyncWorkflow|Daily Sync Workflow]]

## Repo-side / policy tips

- keep binaries out of history (or use org-approved solutions)
- avoid committing generated artifacts
- use `.gitattributes` to prevent broken diffs on binaries

See: [[GitAttributes]], [[GitIgnorePatterns]]

## CI-side tips

- use the right fetch depth:
  - shallow by default if possible
  - full history/tags only for release/versioning jobs

See: [[CiCdIntegration]]

## When performance problems persist

- profile the biggest pain (clone vs status vs CI)
- consider structural changes:
  - split repos (multirepo)
  - or invest in monorepo tooling

See: [[BestPractices/RepositoryManagement/MonorepoVsMultirepo|Monorepo vs Multirepo]]
