---
id: BranchLifecycle
aliases: []
tags: []
---

# Branch Lifecycle

A branch should have a clear lifecycle: create → develop → review → integrate → delete.

## Why lifecycle matters

- prevents branch clutter
- reduces long-running divergence
- lowers merge conflict risk

Related:

- [[Workflows/FeatureBranchWorkflow|Feature Branch Workflow]]
- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]
- [[Workflows/DailySyncWorkflow|Daily Sync Workflow]]
- [[MergevsRebase]]

## Recommended lifecycle (feature branches)

1. Create from `main` (or `develop`, depending on workflow)

```bash
git switch main
git pull --ff-only
git switch -c feature/my-change
```

2. Commit small logical chunks (see [[BestPractices/CommitStrategies/AtomicCommits|Atomic Commits]])

3. Push early to back up work

```bash
git push -u origin feature/my-change
```

4. Open PR, review, iterate

5. Keep branch updated

```bash
git fetch origin
git rebase origin/main
# or merge origin/main depending on policy
```

6. Integrate (merge/squash/rebase policy)

7. Delete branch (local + remote)

```bash
git branch -d feature/my-change
git push origin --delete feature/my-change
```

## Cleaning up stale branches

- periodically prune deleted remote branches:

```bash
git fetch --prune
```

See: [[git-fetch]]

## Special lifecycles

- release branches: exist for a stabilization window, then are merged and removed
- hotfix branches: exist briefly, then merged and removed (see [[Workflows/HotfixWorkflow|Hotfix Workflow]])

## Related notes

- [[BestPractices/BranchingStrategies/LongRunningBranches|Long-Running Branches]]
- [[Workflows/ReleaseWorkflow|Release Workflow]]
