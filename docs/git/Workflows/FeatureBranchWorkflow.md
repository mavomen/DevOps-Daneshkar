---
id: FeatureBranchWorkflow
aliases: []
tags: []
---

# Feature Branch Workflow

A lightweight workflow where each change is developed on its own branch and integrated into `main` via merge (often via PR).

## When to Use

- Small to medium teams
- Most Git hosting platforms (GitHub/GitLab) + PR/MR review
- You want isolation per feature and clear integration points

## Core Idea

- `main` stays stable
- work happens on `feature/...` branches
- integrate via `merge` (or squash/rebase policy)

## Steps (Typical)

1. Update `main`

```bash
git switch main
git pull --ff-only
```

2. Create a feature branch

```bash
git switch -c feature/some-change
```

3. Work and commit

```bash
git status
git diff
git add .
git commit -m "feat: implement some change"
```

4. Push branch

```bash
git push -u origin feature/some-change
```

5. Open PR + review (see [[Workflows/CodeReviewWorkflow|Code Review Workflow]])

6. Integrate (team policy decides)

- Merge commit:
  - `git merge --no-ff feature/some-change`
- Fast-forward (if linear history policy):
  - rebase then `--ff-only`
- Squash merge:
  - hosting platform UI or `git merge --squash`

7. Cleanup

```bash
git switch main
git pull --ff-only
git branch -d feature/some-change
git push origin --delete feature/some-change
```

## Pros / Cons

- Pros:
  - isolates work
  - easy rollback if merged via merge commit
  - supports parallel development well
- Cons:
  - requires discipline around updating branches / resolving conflicts

## Related Notes

- [[Branch]]
- [[MergevsRebase]]
- [[git-branch]]
- [[git-switch]]
- [[git-merge]]
- [[git-rebase]]
- [[Remote]]
