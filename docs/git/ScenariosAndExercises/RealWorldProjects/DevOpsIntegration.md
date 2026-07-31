---
id: DevOpsIntegration
aliases: []
tags: []
---

# DevOps Integration (Real World Project)

A practice project for integrating Git workflows with CI/CD, branch protection, and release automation.

## Goal

- configure CI to run on PRs and main
- enforce quality gates before merge
- optionally build/tag releases

## Prerequisites

- [[CiCdIntegration]]
- [[BranchProtectionRules]]
- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]

## Scenario

Your team wants:

- tests to run on every PR
- main branch protected
- releases tagged and optionally built/published

## Steps

### 1) Add CI pipeline

Pick your platform:

- GitHub Actions workflow file (example in [[CiCdIntegration]])
- GitLab CI file (example in [[CiCdIntegration]])

Ensure it runs on:

- pull requests / merge requests
- pushes to `main`

### 2) Add a `pre-commit` hook (optional)

Use [[GitHooks]] to run quick checks locally.

### 3) Enforce branch protection

Set `main` protection rules:

- PR only
- CI required
- approvals required
- no force push

See: [[BranchProtectionRules]]

### 4) Add release automation (optional)

Example approach:

- on tag `v*`, run release job (build artifacts, publish)

Ensure tags are annotated and pushed:

```bash
git tag -a v0.1.0 -m "Release v0.1.0"
git push origin --tags
```

### 5) Document it

Update `docs/workflow.md` (see [[GitWorkflowTemplate]]):

- merge policy
- CI requirements
- release/tag process

## Acceptance Criteria

- [ ] CI runs on PR and on main
- [ ] Branch protection is enabled and documented
- [ ] Release tagging process is defined
- [ ] Team knows rollback plan

## Related Notes

- [[GitHooks]]
- [[ReleaseWorkflow]]
- [[SecurityPractices]]
- [[EmergencyRecovery]]
