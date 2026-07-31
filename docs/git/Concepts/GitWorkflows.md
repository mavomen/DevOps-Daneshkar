---
id: GitWorkflows
aliases: []
tags: []
---

# Git Workflows

A Git workflow is the combination of branching rules, review rules, and integration strategy a team uses consistently.

## The main workflows (in this vault)

- [[Workflows/GitHubFlow|GitHub Flow]]
- [[Workflows/FeatureBranchWorkflow|Feature Branch Workflow]]
- [[Workflows/GitFlowWorkflow|Git Flow Workflow]]
- [[Workflows/ForkAndPullRequest|Fork and Pull Request]]

## Choose based on constraints

### If you deploy continuously from `main`

- GitHub Flow is usually best.

### If you need scheduled releases / stabilization

- Git Flow (or a simpler release-branch variant) helps.

### If you’re open source / external contributors

- Fork + PR is the standard.

### If team is very small and changes are simple

- Centralized workflow can work, but protect the branch.

## Integration policy (must be explicit)

Pick a default for feature branches:

- merge commits (context preserved)
- squash merge (clean `main`)
- rebase + fast-forward (linear history)

See: [[MergevsRebase]], [[SquashingCommits]]

## Related Notes

- [[CollaborationStrategies]]
- [[BranchProtectionRules]]
- [[CommitMessageBestPractices]]
