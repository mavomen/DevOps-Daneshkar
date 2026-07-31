---
id: SafeGitPractices
aliases: []
tags: []
---

# Safe Git Practices

Habits that prevent emergencies and make recovery easy.

## Daily habits

- check `git status` often
- review diffs before committing:
  - `git diff`
  - `git diff --staged`
- commit small logical units (see [[AtomicCommits]])

## Branch discipline

- don’t work directly on `main`
- push feature branches early for backup
- delete branches after merge

## History safety

- don’t rewrite public/shared history
- prefer `git revert` for shared branch rollbacks
- if you must force push, use `--force-with-lease` and coordinate

## Recovery readiness

- learn `git reflog`
- create backup branches before risky steps

## Related Notes

- [[git-reflog]]
- [[git-revert]]
- [[git-push]]
- [[BranchProtectionRules]]
