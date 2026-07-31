---
id: git-gc
aliases: []
tags: []
---

# git gc

Clean up and optimize the local repository (garbage collection).

## Syntax

```bash
git gc
git gc --aggressive
git gc --prune=<date>
```

## Description

`git gc` packs objects and prunes some unreachable objects according to retention rules, improving performance and reducing disk usage.

## Common usage

### Run default GC

```bash
git gc
```

### Aggressive GC (slower; use occasionally)

```bash
git gc --aggressive
```

## Safety notes

- Avoid running `git gc` while you’re actively trying to recover “lost” commits.
- If you suspect you need reflog recovery, recover first, then optimize.

See: [[git-reflog]]

## Related Notes

- [[Repository]]
- [[Troubleshooting/Prevention/RepositoryHealthChecks|Repository Health Checks]]
- [[Troubleshooting/CommonProblems/SlowGitOperations|Slow Git Operations]]
