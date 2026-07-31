---
id: OnboardingNewDevelopers
aliases: []
tags: []
---

# Onboarding New Developers

A practical checklist for getting a new developer productive quickly and safely.

## Day 1 checklist

- [ ] access to repo and required services
- [ ] Git identity configured:
  - `user.name`, `user.email` (see [[GitConfiguration]])
- [ ] SSH keys set (or HTTPS tokens):
  - see [[SshKeysSetup]]
- [ ] clone the repository:
  - [[git-clone]]
- [ ] run tests locally:
  - document in README (see [[DocumentationStandards]])

## Workflow training (minimum)

- branch naming conventions:
  - [[BranchNamingConventions]]
- feature branch workflow:
  - [[Workflows/FeatureBranchWorkflow|Feature Branch Workflow]]
- code review expectations:
  - [[CodeReviewGuidelines]]
- safe undo vs dangerous undo:
  - [[git-revert]] vs [[git-reset]]
- recovery basics:
  - [[git-reflog]]

## Team rules recap

- no direct pushes to `main`
- PR required with passing CI
- merge method policy (squash/merge/rebase)
- secrets policy (never commit secrets)

See: [[TeamGuidelines]], [[SecurityPractices]]

## Useful starter commands

```bash
git status -sb
git fetch --prune
git pull --ff-only
git switch -c feature/your-first-task
git push -u origin feature/your-first-task
```

## Related Notes

- [[GitConfiguration]]
- [[SshKeysSetup]]
- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]
- [[BranchProtectionRules]]
