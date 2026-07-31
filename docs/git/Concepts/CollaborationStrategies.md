---
id: CollaborationStrategies
aliases: []
tags: []
---

# Collaboration Strategies

Collaboration strategies are conventions teams adopt to work safely in a distributed system like Git.

## Core building blocks

- [[Remote]] (origin/upstream)
- [[Branch]] (feature work isolation)
- integration choices: [[MergevsRebase]]
- code review process: [[Workflows/CodeReviewWorkflow|Code Review Workflow]]

## Strategy 1: Feature branches + PRs (most common)

- Everyone branches off `main`
- Work happens on `feature/...`
- PR is reviewed + CI checked
- Merge to `main` via the platform

See: [[Workflows/FeatureBranchWorkflow|Feature Branch Workflow]], [[Workflows/GitHubFlow|GitHub Flow]]

## Strategy 2: Fork + Pull Request (open source)

- Contributors fork
- `origin` = fork, `upstream` = canonical
- PR from fork branch → upstream `main`

See: [[Workflows/ForkAndPullRequest|Fork and Pull Request]], [[UpstreamAndOrigin]]

## Strategy 3: Git Flow (release control)

- `main` = production
- `develop` = integration
- `release/*` and `hotfix/*` branches

See: [[Workflows/GitFlowWorkflow|Git Flow Workflow]]

## Strategy 4: Centralized style (simple but conflict-prone)

- Everyone pushes to `main` (or a shared branch)
- Requires strict coordination and protections

## Practical rules that prevent pain

- protect `main` (PR-only, no force push)
- sync frequently (`git fetch --prune`)
- keep branches short-lived
- prefer `git revert` for shared rollbacks

Related:

- [[BranchProtectionRules]]
- [[Workflows/DailySyncWorkflow|Daily Sync Workflow]]
- [[git-revert]]
