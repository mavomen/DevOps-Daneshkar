---
id: MergeVsRebaseStrategy
aliases: []
tags: []
---

# Merge vs Rebase Strategy

A team strategy for integrating work consistently.

## First: define your team goals

Choose what you want more:

- a clean, linear `main`
- full branch context preserved
- minimal risk for non-expert Git users
- easy bisecting/debugging

See: [[MergevsRebase]]

## Recommended team-safe defaults

### Shared branches (`main`, `develop`, `release/*`)

- avoid rewriting history
- prefer merge commits or squash merges via PR tooling
- rollback via [[git-revert]]

### Feature branches

- rebase to keep up to date (optional policy)
- interactive rebase to clean history (optional)
- if rebasing pushed feature branches, use:

```bash
git push --force-with-lease
```

## Common policy choices

### Policy A: Squash merge everything to main (very common)

- developers commit freely on feature branches
- PR merges squash into a single commit on `main`
- `main` stays clean and easy to revert

### Policy B: Merge commits on main (preserve context)

- each PR creates a merge commit
- commit history shows parallel development clearly

### Policy C: Rebase and merge (linear main, but requires discipline)

- requires careful coordination to avoid rewriting shared history
- often enforced by platform options rather than manual CLI merges

## Conflict policy

- resolve conflicts on the feature branch before merging
- document non-trivial resolutions in PR description

See: [[ConflictResolution]]

## Related Notes

- [[Workflows/GitHubFlow|GitHub Flow]]
- [[Workflows/FeatureBranchWorkflow|Feature Branch Workflow]]
- [[Workflows/GitFlowWorkflow|Git Flow Workflow]]
- [[BranchProtectionRules]]
- [[git-revert]]
