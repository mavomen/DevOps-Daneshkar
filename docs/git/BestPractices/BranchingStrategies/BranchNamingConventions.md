---
id: BranchNamingConventions
aliases: []
tags: []
---

# Branch Naming Conventions

Branch names are lightweight metadata. Good naming improves collaboration, CI visibility, and review.

## Goals

- indicate intent quickly
- support automation (CI rules, release tooling)
- keep names consistent across the team

Related:

- [[Branch]]
- [[Workflows/FeatureBranchWorkflow|Feature Branch Workflow]]
- [[Workflows/GitHubFlow|GitHub Flow]]
- [[Workflows/GitFlowWorkflow|Git Flow Workflow]]

## Recommended patterns

### Feature work

- `feature/<short-description>`
- `feat/<short-description>`

Examples:

- `feature/user-search`
- `feat/auth-refresh`

### Bug fixes

- `fix/<short-description>`
- `bugfix/<short-description>`

Examples:

- `fix/null-pointer-on-login`

### Hotfixes

- `hotfix/<issue-or-description>`

Example:

- `hotfix/checkout-crash`

### Chores / maintenance

- `chore/<short-description>`
- `refactor/<short-description>`
- `docs/<short-description>`

Examples:

- `chore/update-deps`
- `docs/api-usage`

## Optional: include ticket IDs

If you use an issue tracker:

- `feature/PROJ-123-user-search`
- `fix/PROJ-981-null-userid`

## Naming rules (practical)

- use lowercase + hyphens
- avoid spaces and underscores (unless your team prefers underscores)
- keep it short (avoid long sentences)
- avoid personal names in branch names (use authorship in PRs instead)

## Related commands

- [[git-branch]]
- [[git-switch]]
- [[git-push]]
