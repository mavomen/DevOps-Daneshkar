---
id: TeamProjectSetup
aliases: []
tags: []
---

# Team Project Setup (Real World Project)

A guided exercise for setting up a team repository with safe defaults.

## Goal

- create a repo with a clean structure
- define workflow and branch rules
- set up basic PR process + protection expectations
- create first release tag

## Prerequisites

- [[GitConfiguration]]
- [[GitAliases]] (optional)
- Familiar with:
  - [[Workflows/FeatureBranchWorkflow|Feature Branch Workflow]]
  - [[BranchProtectionRules]]
  - [[CommitMessageBestPractices]]

## Scenario

You are starting a new team project and want the repo to be easy to clone/run/test, and safe to collaborate on.

## Steps

### 1) Initialize repo structure

```bash
mkdir team-project
cd team-project
git init --initial-branch=main
```

Create baseline files:

- `README.md`
- `.gitignore` (see [[GitIgnorePatterns]])
- `docs/workflow.md` (use [[GitWorkflowTemplate]])

Example:

```bash
printf "# Team Project\n" > README.md
printf ".env\nnode_modules/\ndist/\n" > .gitignore
mkdir -p docs
```

### 2) First commit

```bash
git add .
git commit -m "chore: initial commit"
```

### 3) Create remote repo (platform UI) and connect

```bash
git remote add origin <url>
git push -u origin main
```

### 4) Define team workflow (docs)

- Decide merge strategy: squash vs merge commit
- Decide branch naming rules
- Decide CI expectations

Store in `docs/workflow.md`.

### 5) Add PR template (optional but recommended)

Use: [[PullRequestTemplate]]

### 6) Branch protection (platform settings)

Set (recommended):

- PR required for `main`
- CI checks required
- no force push
- require approvals

See: [[BranchProtectionRules]]

### 7) Add a sample feature using the workflow

```bash
git switch -c feature/sample-endpoint
# add a small file
mkdir -p src
printf "export const hello = () => 'hello';\n" > src/hello.js
git add src/hello.js
git commit -m "feat: add hello helper"
git push -u origin feature/sample-endpoint
```

Open PR and merge.

### 8) Tag first release

```bash
git switch main
git pull --ff-only
git tag -a v0.1.0 -m "Release v0.1.0"
git push origin --tags
```

## Acceptance Criteria

- [ ] Repo has README + .gitignore + workflow doc
- [ ] Branch protection configured (documented)
- [ ] At least one PR merged using team policy
- [ ] Release tag exists and is pushed

## Related Notes

- [[RepositoryStructure]]
- [[GitWorkflowTemplate]]
- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]
- [[git-tag]]
