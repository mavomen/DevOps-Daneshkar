---
id: HotfixWorkflow
aliases: []
tags: []
---

# Hotfix Workflow

An urgent fix workflow for production issues: branch from `main`, fix, release, then propagate the fix to other branches.

## When to Use

- Production bug/security issue
- You need a fast path to a tagged release

## Steps

1. Create hotfix branch from `main`

```bash
git switch main
git pull --ff-only
git switch -c hotfix/critical-fix
```

2. Implement fix + tests, then commit

```bash
git add .
git commit -m "fix: resolve critical issue"
```

3. Merge hotfix back to `main` and tag

```bash
git switch main
git pull --ff-only
git merge --no-ff hotfix/critical-fix
git tag -a vX.Y.Z -m "Hotfix vX.Y.Z"
git push origin main --tags
```

4. Propagate to `develop` (Git Flow) or other long-lived branches

Option A (merge):

```bash
git switch develop
git pull --ff-only
git merge --no-ff hotfix/critical-fix
git push origin develop
```

Option B (cherry-pick the hotfix commit(s)):

```bash
git switch develop
git cherry-pick <hotfix-commit-hash>
git push origin develop
```

5. Cleanup

```bash
git branch -d hotfix/critical-fix
git push origin --delete hotfix/critical-fix
```

## Related Notes

- [[git-merge]]
- [[git-tag]]
- [[git-cherry-pick]]
- [[Workflows/ReleaseWorkflow|Release Workflow]]
