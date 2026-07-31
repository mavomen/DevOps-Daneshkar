---
id: GitFlowWorkflow
aliases: []
tags: []
---

# Git Flow Workflow

A structured workflow with long-lived branches (`main`, `develop`) and supporting `feature/`, `release/`, `hotfix/` branches.

## When to Use

- You do scheduled releases (not continuous deploy from `main`)
- You need a stabilization phase before release
- You accept more branching complexity for clearer release control

## Branch Roles

- `main`: production releases only (tagged)
- `develop`: integration branch for upcoming release
- `feature/*`: new work branched from `develop`
- `release/*`: stabilization branched from `develop`
- `hotfix/*`: urgent fixes branched from `main`

## Typical Feature Flow

```bash
git switch develop
git pull --ff-only
git switch -c feature/my-feature
# commit work
git push -u origin feature/my-feature
# PR into develop
```

## Release Flow (High Level)

1. Create release branch from `develop`

```bash
git switch develop
git pull --ff-only
git switch -c release/v1.2.0
git push -u origin release/v1.2.0
```

2. Stabilize on release branch (bugfixes only)

3. Merge release into `main`, tag, and merge back into `develop`

```bash
git switch main
git pull --ff-only
git merge --no-ff release/v1.2.0
git tag -a v1.2.0 -m "Release v1.2.0"
git push origin main --tags

git switch develop
git pull --ff-only
git merge --no-ff release/v1.2.0
```

## Hotfix Flow (High Level)

See [[Workflows/HotfixWorkflow|Hotfix Workflow]]

## Related Notes

- [[Branch]]
- [[Remote]]
- [[git-merge]]
- [[git-tag]]
- [[git-cherry-pick]]

````

---

## `Workflows/CentralizedWorkflow.md`

```md
# Centralized Workflow

A “single shared branch” workflow that mimics centralized VCS habits (often all work goes into `main`).

## When to Use

- Very small teams
- Simple projects
- You don’t need heavy parallel development

## Core Idea

- Everyone pulls `main`, commits locally, and pushes back to `main`
- Collaboration depends heavily on frequent syncing and conflict resolution

## Steps

1. Update local `main`

```bash
git switch main
git pull --ff-only
````

2. Make changes and commit

```bash
git add .
git commit -m "fix: update behavior"
```

3. Push

```bash
git push origin main
```

## If Push Is Rejected (Remote moved)

Option A (merge-based):

```bash
git pull
git push
```

Option B (rebase-based, cleaner history):

```bash
git pull --rebase
git push
```

## Pros / Cons

- Pros:
  - simple mental model
- Cons:
  - more conflicts on shared branch
  - harder to review changes before integration
  - riskier without branch protection

## Related Notes

- [[DistributedvsCentralized]]
- [[Remote]]
- [[MergevsRebase]]
- [[Workflows/DailySyncWorkflow|Daily Sync Workflow]]
