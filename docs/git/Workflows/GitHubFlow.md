---
id: GitHubFlow
aliases: []
tags: []
---

# GitHub Flow

A simple workflow centered around a stable `main` branch and short-lived branches integrated via pull requests.

## When to Use

- Continuous delivery / frequent deploys
- You can deploy from `main`
- You want minimal branching complexity

## Rules of Thumb

- `main` is always deployable
- every change is a branch + PR
- merge to `main` triggers deploy (often CI/CD)

## Steps

1. Create branch from `main`

```bash
git switch main
git pull --ff-only
git switch -c feature/short-description
```

2. Commit frequently

```bash
git add .
git commit -m "feat: add X"
```

3. Push and open PR

```bash
git push -u origin feature/short-description
```

4. Review + CI + approval (see [[Workflows/CodeReviewWorkflow|Code Review Workflow]])

5. Merge to `main` (policy: merge commit / squash / rebase)

6. Deploy from `main`

7. Delete branch

```bash
git push origin --delete feature/short-description
git branch -d feature/short-description
```

## Common Policies

- “Squash and merge” for a very clean `main`
- “Merge commit” to preserve branch context
- “Rebase and merge” for linear history

See: [[MergevsRebase]]

## Related Notes

- [[Remote]]
- [[Workflows/FeatureBranchWorkflow|Feature Branch Workflow]]
- [[Workflows/DailySyncWorkflow|Daily Sync Workflow]]
