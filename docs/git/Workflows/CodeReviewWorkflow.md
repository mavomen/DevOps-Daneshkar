---
id: CodeReviewWorkflow
aliases: []
tags: []
---

# Code Review Workflow

A workflow for submitting changes for review before integration, typically via PR/MR.

## Goals

- catch bugs early
- enforce standards
- share context and knowledge
- protect `main`

## Steps

1. Create a branch and commit changes

```bash
git switch main
git pull --ff-only
git switch -c feature/small-change

git add .
git commit -m "feat: implement change"
```

2. Push branch and open PR

```bash
git push -u origin feature/small-change
```

3. Review cycle

- reviewer comments
- author updates branch with new commits (or rebases/squashes depending on policy)

4. Keep branch updated during long reviews

```bash
git fetch origin
git rebase origin/main
git push --force-with-lease
```

5. Merge (policy-based)

- merge commit / squash / rebase merge

6. Post-merge cleanup

```bash
git switch main
git pull --ff-only
git branch -d feature/small-change
git push origin --delete feature/small-change
```

## Good Review Practices (Short)

- keep PRs small and focused
- include “what/why/how to test”
- reviewers focus on correctness, security, maintainability

## Related Notes

- [[Workflows/FeatureBranchWorkflow|Feature Branch Workflow]]
- [[MergevsRebase]]
- [[git-push]]
- [[git-fetch]]
