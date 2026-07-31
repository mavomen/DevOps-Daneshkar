---
id: ForkAndPullRequest
aliases: []
tags: []
---

# Fork and Pull Request Workflow

A collaboration workflow common in open source: contributors work in forks and submit pull requests to the upstream repo.

## When to Use

- Open source projects
- When contributors do not have push access to the canonical repo

## Remotes Convention

- `origin` = your fork
- `upstream` = canonical repo

See: [[UpstreamAndOrigin]]

## Setup (Once)

```bash
git clone https://github.com/you/project.git
cd project

git remote add upstream https://github.com/original/project.git
git fetch upstream
```

## Daily Sync

```bash
git switch main
git fetch upstream
git merge upstream/main
git push origin main
```

## Make a Change

```bash
git switch -c feature/my-fix
# edit files
git add .
git commit -m "fix: correct behavior"
git push -u origin feature/my-fix
```

Then open a PR from `you:feature/my-fix` → `original:main`.

## Keeping Your Branch Updated During Review

```bash
git fetch upstream
git rebase upstream/main
git push --force-with-lease origin feature/my-fix
```

## Related Notes

- [[Remote]]
- [[git-remote]]
- [[git-fetch]]
- [[git-push]]
- [[git-rebase]]
- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]
