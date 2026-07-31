---
id: CommitMessageTemplates
aliases: []
tags: []
---

# Commit Message Templates

Commit message templates help teams write consistent, high-signal commit messages.

## Option A: A Git commit template file (recommended)

1. Create a template file, e.g. `~/.config/git/commit-template.txt`

Example template:

```txt
# <type>(scope): summary
#
# Why:
# -
#
# What:
# -
#
# Notes:
# - breaking change? migration steps?
#
# Refs:
# -
```

2. Configure Git to use it:

```bash
git config --global commit.template ~/.config/git/commit-template.txt
```

Now when you run `git commit` (without `-m`), your editor opens with the template.

Related: [[GitConfiguration]], [[git-commit]]

## Option B: Project-local template (team-shared)

In your repo, store a template (example path):

- `.github/commit-template.txt` or `docs/commit-template.txt`

Then set locally:

```bash
git config commit.template .github/commit-template.txt
```

## Option C: Commit-msg hook enforcement (team policy)

Use a `commit-msg` hook to enforce format.

See: [[GitHooks]]

## Template examples

### Minimal

```txt
<type>: <summary>

Why:
- ...

Refs:
- ...
```

### Conventional-style

```txt
feat(scope): short summary

Context:
- ...

Testing:
- ...

Refs:
- ...
```

## Related notes

- [[BestPractices/CommitStrategies/CommitMessageBestPractices|Commit Message Best Practices]]
- [[GitConfiguration]]
- [[GitHooks]]
