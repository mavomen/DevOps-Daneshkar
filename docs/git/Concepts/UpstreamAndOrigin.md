---
id: UpstreamAndOrigin
aliases: []
tags: []
---

# Upstream and Origin

In Git, **`origin`** is a conventional name for a remote, and **upstream** usually refers to either:

1. A remote named `upstream` (common in fork workflows), and/or
2. The _upstream branch_ your local branch tracks (e.g., `main` tracking `origin/main`)

This note explains both meanings clearly.

## Origin (Remote)

When you clone a repository, Git typically creates a remote named `origin` automatically:

```bash
git remote -v
# origin  https://github.com/you/repo.git (fetch)
# origin  https://github.com/you/repo.git (push)
```

Concept link:

- [[Remote]]

## Upstream (Remote) — Fork Workflow Convention

If you fork a repo, a common convention is:

- `origin` = your fork
- `upstream` = the original repo you forked from

Example:

```bash
# you cloned your fork → origin exists
git remote -v

# add upstream (the canonical repo)
git remote add upstream https://github.com/original/repo.git

# fetch upstream changes
git fetch upstream
```

## Upstream (Branch) — Tracking Relationship

A **local branch** can track a **remote-tracking branch**:

- local: `main`
- upstream branch: `origin/main`

Check tracking:

```bash
git branch -vv
```

Typical output pattern:

```txt
* main  abc1234 [origin/main] Some message
```

### Setting upstream on first push

```bash
git push -u origin feature/my-branch
```

Now these work without extra args:

```bash
git pull
git push
```

### Setting upstream explicitly

```bash
git branch --set-upstream-to=origin/main main
# or shorthand (if supported in your git)
git branch -u origin/main main
```

## Why This Matters

- `git pull` depends on upstream tracking (unless you pass remote/branch)
- `git push` often depends on upstream tracking (unless you pass remote/branch)
- Fork workflows depend on separating “my fork” vs “canonical source”

## Typical Fork Sync Routine (Clean + Simple)

```bash
git fetch upstream
git switch main
git merge upstream/main
git push origin main
```

> Some teams prefer `rebase` here; the merge is the simplest safe default on a shared `main`.

## Related Notes

- [[git-remote]]
- [[git-fetch]]
- [[git-pull]]
- [[git-push]]
- [[Branch]]
- [[Remote]]
