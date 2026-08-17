---
id: ReleaseManagement
aliases: []
tags: []
---

# Release Management

A set of practices for shipping versions reliably (tags, changelogs, branching, hotfixes).

## Core release elements

- versioning scheme (often semver)
- release notes / changelog
- tags (source of truth for “what shipped”)
- rollback plan

See: [[Workflows/ReleaseWorkflow|Release Workflow]], [[git-tag]]

## Tag policy (recommended)

- use annotated tags:

```bash
git tag -a vX.Y.Z -m "Release vX.Y.Z"
git push origin --tags
```

## Release checklist

- [ ] CI green on release candidate
- [ ] version bump committed
- [ ] changelog updated
- [ ] tag created and pushed
- [ ] artifacts built/published
- [ ] deployment completed
- [ ] rollback plan documented

## Hotfix procedure

- branch from `main`: `hotfix/...`
- merge hotfix back to `main`, tag patch version
- propagate to integration branch (merge or cherry-pick)

See: [[Workflows/HotfixWorkflow|Hotfix Workflow]]

## Release branches (if using them)

- allow only bug fixes and release prep
- merge to `main` and back to integration branch
- delete after release

See: [[Workflows/GitFlowWorkflow|Git Flow Workflow]]

## Related Notes

- [[git-tag]]
- [[git-cherry-pick]]
- [[RollbackProcedures]]
