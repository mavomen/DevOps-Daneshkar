---
id: LegacyCodeIntegration
aliases: []
tags: []
---

# Legacy Code Integration (Real World Project)

A guided exercise for introducing Git to an existing (legacy) codebase or integrating a legacy module into a modern repo.

## Goal

- bring existing code into Git cleanly
- avoid committing generated artifacts
- create a readable initial history baseline
- set up safe branching for refactors

## Prerequisites

- [[GitIgnorePatterns]]
- [[RepositoryStructure]]
- [[AtomicCommits]]
- Familiar with:
  - [[git-init]]
  - [[git-add]]
  - [[git-commit]]

## Scenario

You received a ZIP folder of an old project with no Git history. You must integrate it into a new repo and prepare it for maintenance/refactor.

## Steps

### 1) Create a new repository and add `.gitignore`

```bash
mkdir legacy-project
cd legacy-project
git init --initial-branch=main
```

Create `.gitignore` tailored to the project language/tooling.

### 2) Add the legacy code

- copy legacy files into the repo working directory

### 3) Commit as an “import” baseline (single commit)

```bash
git add .
git commit -m "chore: import legacy codebase"
```

### 4) Add repository structure improvements (separate commits)

Examples (separate commits):

- add README explaining how to run
- add formatting or lint config
- add tests harness skeleton
- add CI config

```bash
git add README.md
git commit -m "docs: add README and run instructions"
```

### 5) Start refactor work on a branch

```bash
git switch -c refactor/normalize-layout
```

Keep refactor commits atomic and testable.

### 6) Keep the branch synced

```bash
git fetch origin --prune
git rebase origin/main
```

## Acceptance Criteria

- [ ] Legacy import is one clear baseline commit
- [ ] No secrets or generated artifacts committed
- [ ] Refactors happen on branches with review

## Related Notes

- [[GitIgnorePatterns]]
- [[SecurityPractices]]
- [[Workflows/FeatureBranchWorkflow|Feature Branch Workflow]]
