---
id: PairProgrammingWorkflow
aliases: []
tags: []
---

# Pair Programming Workflow

A collaboration workflow where two developers work together on the same change, with clear ownership of commits and a clean integration path.

## When to Use

- complex or risky changes
- onboarding / mentorship
- debugging hard issues

## Two Practical Models

### A) One driver, one branch (simplest)

- One person (driver) owns the branch + commits
- The navigator reviews continuously
- Use normal PR review at the end (optional but recommended)

Workflow:

```bash
git switch main
git pull --ff-only
git switch -c feature/pair-session
# commit as you go
git push -u origin feature/pair-session
```

### B) Shared branch with strict coordination

If both commit to the same branch, adopt rules:

- frequent `git fetch` + `git pull --rebase`
- no rewriting history unless both agree
- prefer `--force-with-lease` only with coordination

## Session Hygiene

- Start with a clean working tree: `git status`
- Make small, readable commits
- Run tests together before pushing
- End with a PR and summary

## Suggested Commit Pattern

- commits reflect logical steps (not “WIP spam”)
- if you did create noisy commits, clean up on a private branch:
  - `git rebase -i` (then push with coordination)

## Related Notes

- [[Workflows/DailySyncWorkflow|Daily Sync Workflow]]
- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]
- [[git-rebase]]
- [[git-push]]
- [[git-fetch]]
