---
id: MonorepoVsMultirepo
aliases: []
tags: []
---

# Monorepo vs Multirepo

This note outlines tradeoffs between storing many projects in one repository (monorepo) vs multiple repositories (multirepo).

## Monorepo (one repo)

### Pros

- atomic cross-project changes in one commit/PR
- unified tooling and CI patterns
- simpler dependency version alignment
- easier global refactors

### Cons

- repo can become large/slow without good tooling
- access control is harder (everyone sees everything)
- CI can be expensive if not scoped

## Multirepo (many repos)

### Pros

- smaller repos, faster clone/fetch
- clearer ownership boundaries
- easier access control per project
- independent release cadence

### Cons

- cross-repo changes are harder (coordination)
- duplicated tooling/config across repos
- dependency management becomes heavier

## Decision signals

Choose monorepo when:

- teams frequently change multiple components together
- you can invest in CI optimization + tooling

Choose multirepo when:

- components are truly independent
- access control / separation is important
- you want independent release cycles

## Git workflow impact

- Monorepo benefits from strong branch protection and CI discipline:
  - [[BestPractices/BranchingStrategies/BranchProtectionRules|Branch Protection Rules]]
  - [[CiCdIntegration]]
- Both benefit from:
  - good commit hygiene (see [[BestPractices/CommitStrategies/AtomicCommits|Atomic Commits]])

## Related notes

- [[BestPractices/RepositoryManagement/LargeRepositoryHandling|Large Repository Handling]]
- [[BestPractices/RepositoryManagement/RepositoryStructure|Repository Structure]]
