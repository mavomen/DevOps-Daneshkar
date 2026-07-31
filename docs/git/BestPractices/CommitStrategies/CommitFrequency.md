---
id: CommitFrequency
aliases: []
tags: []
---

# Commit Frequency

Commit often enough to create safe checkpoints, but not so often that history becomes noisy and unreviewable.

## Good default (most teams)

- commit when you complete a small logical unit (fits in a review)
- commit when you reach a stable point (tests pass / build works)
- avoid long gaps between commits on feature branches

Related:

- [[BestPractices/CommitStrategies/AtomicCommits|Atomic Commits]]
- [[Workflows/FeatureBranchWorkflow|Feature Branch Workflow]]

## Practical guidance

### Commit when…

- a function/module reaches a coherent state
- you’ve added tests for a behavior
- you’re about to refactor further and want a safe checkpoint
- you’re about to switch context (meeting/interruptions)

### Avoid committing when…

- the commit breaks builds/tests (unless your team explicitly allows it on private branches)
- the commit message would be “WIP” because the change is unclear
- you’ve mixed unrelated changes (split first)

## Handling WIP responsibly

If you truly need to park work:

- prefer `git stash` for short interruptions

```bash
git stash push -m "WIP before context switch"
```

- or use a clearly marked WIP commit on a private branch (team policy)

If you created messy WIP commits, clean up before sharing:

- interactive rebase (private branch):

```bash
git rebase -i
```

## Team policy tip

For PRs, a good target is:

- enough commits to show meaningful steps
- not so many that review becomes “commit archaeology”

If your platform supports it, you can squash on merge while still committing frequently during development.

## Related notes

- [[git-stash]]
- [[git-rebase]]
- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]
