---
id: GitWorkflowTemplate
aliases: []
tags: []
---

# Git Workflow Template

A team policy template you can adapt per repository. Put this into `docs/workflow.md` or `CONTRIBUTING.md`.

## Template

```md
# Git Workflow

## Branch model

- Default branch: `main`
- Long-running branches (if any): `develop` / `release/*` / `hotfix/*`
- Feature branches: `feature/<short-description>`

## Branch naming

- `feature/...`, `fix/...`, `hotfix/...`, `release/...`, `chore/...`
- Optional: include ticket IDs (e.g., `feature/PROJ-123-login`)

## Commit messages

- Use conventional-ish format: `type(scope): summary`
- Prefer atomic commits
- Avoid "WIP" commits on shared branches

## Daily sync

- Prefer `git fetch --prune`
- Integrate via:
  - feature branches: rebase onto `origin/main` (recommended)
  - shared branches: merge only (or policy-defined)

## Pull requests

- PR required to merge to `main`
- Required checks:
  - CI tests
  - lint
- Required approvals: 1–2
- Merge method: squash | merge commit | rebase merge (pick one)

## Branch protection

- No direct push to `main`
- No force push to `main`
- Delete branches after merge

## Releases

- Tag releases: `vX.Y.Z`
- Use annotated tags
- Release checklist:
  - version bump
  - changelog update
  - tag + push tags

## Hotfixes

- Branch from `main`: `hotfix/<name>`
- Merge back to `main`, tag, then propagate to integration branch

## Recovery / safety

- Use `git revert` on shared branches
- Use `git reflog` for recovery when something goes wrong
```

## Related Notes

- [[Workflows/GitHubFlow|GitHub Flow]]
- [[Workflows/GitFlowWorkflow|Git Flow Workflow]]
- [[BestPractices/BranchingStrategies/BranchProtectionRules|Branch Protection Rules]]
- [[BestPractices/CommitStrategies/AtomicCommits|Atomic Commits]]
- [[git-revert]]
- [[git-reflog]]
