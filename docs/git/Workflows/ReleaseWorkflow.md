---
id: ReleaseWorkflow
aliases: []
tags: []
---

# Release Workflow

A workflow for preparing and shipping a versioned release, usually involving tagging and sometimes a release branch.

## When to Use

- You ship versioned releases (`v1.2.0`)
- You need stabilization time before release
- You want predictable release artifacts

## Two Common Approaches

### A) Release directly from `main` (simple)

1. Ensure `main` is up to date
2. Bump version + changelog
3. Tag release
4. Push tag

```bash
git switch main
git pull --ff-only
# edit version files
git add .
git commit -m "chore(release): v1.2.0"
git tag -a v1.2.0 -m "Release v1.2.0"
git push origin main --tags
```

### B) Release branch (Git Flow style)

See [[Workflows/GitFlowWorkflow|Git Flow Workflow]].

## Notes on Tags

- Prefer annotated tags for releases: `git tag -a ...`
- Push tags explicitly: `git push --tags`

## Related Notes

- [[git-tag]]
- [[git-log]]
- [[Workflows/HotfixWorkflow|Hotfix Workflow]]
