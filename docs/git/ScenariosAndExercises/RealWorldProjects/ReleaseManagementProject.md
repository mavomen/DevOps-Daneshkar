---
id: ReleaseManagementProject
aliases: []
tags: []
---

# Release Management Project (Real World Project)

Practice creating a release with versioning, changelog, tagging, and rollback planning.

## Goal

- create a release plan
- update version + changelog
- tag the release
- publish tags
- define rollback procedure

## Prerequisites

- [[Workflows/ReleaseWorkflow|Release Workflow]]
- [[ReleaseManagement]]
- [[git-tag]]
- [[RollbackProcedures]]

## Scenario

Your team is shipping `v1.2.0`. You must prepare the release and ensure it is reproducible and rollback-able.

## Steps

### 1) Ensure `main` is green and up-to-date

```bash
git switch main
git pull --ff-only
```

### 2) Create release prep commit

- bump version (wherever your project stores it)
- update `CHANGELOG.md`

```bash
git add CHANGELOG.md <version-file>
git commit -m "chore(release): v1.2.0"
```

### 3) Create annotated tag

```bash
git tag -a v1.2.0 -m "Release v1.2.0"
```

### 4) Push `main` and tags

```bash
git push origin main --tags
```

### 5) Write rollback plan (as documentation)

Create `docs/rollback.md` containing:

- last known good tag
- revert strategy (revert commits vs deploy previous tag)
- who approves the rollback

See: [[RollbackProcedures]]

## Acceptance Criteria

- [ ] Annotated tag exists for release
- [ ] Changelog updated and committed
- [ ] Tags are pushed to remote
- [ ] Rollback plan exists

## Related Notes

- [[git-log]]
- [[git-show]]
- [[DisasterRecovery]]
