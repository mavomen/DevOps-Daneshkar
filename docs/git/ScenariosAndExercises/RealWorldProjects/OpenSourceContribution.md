---
id: OpenSourceContribution
aliases: []
tags: []
---

# Open Source Contribution (Real World Project)

A guided exercise for contributing to an open source repo using the fork + pull request workflow.

## Goal

- fork a repo
- clone your fork
- add `upstream`
- create a feature branch
- make a clean change
- open a PR
- keep branch updated until merged

## Prerequisites

- [[GitInstallation]]
- [[GitConfiguration]]
- [[SshKeysSetup]] (optional but recommended)
- You understand:
  - [[Remote]]
  - [[UpstreamAndOrigin]]
  - [[Workflows/ForkAndPullRequest|Fork and Pull Request]]

## Scenario

You found a small documentation typo in an open source project and want to fix it properly.

## Steps

### 1) Fork the repository (on the platform UI)

- Fork `original/project` into `your/project`

### 2) Clone your fork

```bash
git clone git@github.com:YOURUSER/project.git
cd project
```

Verify remotes:

```bash
git remote -v
```

### 3) Add upstream

```bash
git remote add upstream git@github.com:ORIGINAL/project.git
git fetch upstream
```

### 4) Sync your main with upstream

```bash
git switch main
git merge upstream/main
git push origin main
```

### 5) Create a branch for your change

```bash
git switch -c fix/docs-typo
```

### 6) Make the change

- edit `README.md` (or relevant docs)

Check diff:

```bash
git diff
```

### 7) Commit (atomic + good message)

```bash
git add README.md
git commit -m "docs: fix typo in README"
```

See: [[CommitMessageBestPractices]], [[AtomicCommits]]

### 8) Push branch to your fork

```bash
git push -u origin fix/docs-typo
```

### 9) Open a PR (platform UI)

Base: `ORIGINAL/project:main`  
Compare: `YOUR/project:fix/docs-typo`

Include in PR description:

- what changed
- why it matters
- how to verify

Template: [[PullRequestTemplate]]

### 10) Address review feedback

- commit more changes (preferred), or
- amend/squash (only if project requests)

### 11) Keep your branch up-to-date (if PR takes time)

```bash
git fetch upstream
git rebase upstream/main
git push --force-with-lease origin fix/docs-typo
```

### 12) Cleanup after merge

```bash
git switch main
git fetch upstream
git merge upstream/main
git push origin main

git branch -d fix/docs-typo
git push origin --delete fix/docs-typo
```

## Acceptance Criteria

- [ ] `origin` points to your fork; `upstream` points to canonical
- [ ] PR is small, clear, and passes CI
- [ ] Branch is deleted after merge
- [ ] You can explain why `--force-with-lease` is safer than `--force`

## Related Notes

- [[Workflows/ForkAndPullRequest|Fork and Pull Request]]
- [[git-remote]]
- [[git-fetch]]
- [[git-push]]
- [[git-rebase]]
