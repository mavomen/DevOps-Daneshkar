---
id: BranchProtectionRules
aliases: []
tags: []
---

# Branch Protection Rules

Branch protection prevents risky changes from being pushed directly to critical branches like `main`.

## Goals

- keep `main` always deployable (GitHub Flow style)
- require review and CI checks
- prevent force pushes and history rewrites on shared branches

Related:

- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]
- [[Workflows/GitHubFlow|GitHub Flow]]
- [[Workflows/GitFlowWorkflow|Git Flow Workflow]]

## Typical protection rules for `main`

### Required before merge

- require PR (no direct push)
- require approvals (e.g., 1–2 reviewers)
- require CI status checks to pass
- require branch to be up-to-date before merge (optional, can increase rebasing)
- require signed commits (optional)
- require conversation resolution (no unresolved review threads)

### History safety

- disallow force pushes
- disallow branch deletion (or allow only maintainers)
- restrict who can push

### Merge strategy policy (choose one)

- allow squash merge only (clean linear history)
- allow merge commits (preserve context)
- allow rebase merge (linear but can rewrite)

See: [[MergevsRebase]]

## Protections for long-lived branches

If you use `develop` (Git Flow), protect it too:

- required CI checks
- PR-only merges
- allow force push? (usually no)

## Local habits that support protection

- use `git push --force-with-lease` only on private feature branches and only with coordination
- prefer `git revert` over `git reset` on shared branches

Related commands:

- [[git-push]]
- [[git-revert]]
- [[git-reset]]
