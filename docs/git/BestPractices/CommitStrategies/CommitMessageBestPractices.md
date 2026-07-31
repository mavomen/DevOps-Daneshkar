---
id: CommitMessageBestPractices
aliases: []
tags: []
---

# Commit Message Best Practices

Commit messages are part of your project’s documentation. They should explain **what** changed and **why**, not just **how**.

## Goals of a good commit message

- makes `git log` readable
- helps reviewers understand intent
- improves debugging (especially with `git bisect`)
- simplifies release notes / changelogs

Related:

- [[git-commit]]
- [[git-log]]
- [[git-bisect]]
- [[GitHistory]]

## Recommended format (classic)

```txt
<type>(optional-scope): short summary in imperative mood

Why this change is needed.
What alternatives were considered (if relevant).
How it impacts behavior, risks, or migrations.

Refs: #123
```

### Examples

```txt
feat(auth): support refresh token rotation

Prevents long-lived sessions from being hijacked.
Adds rotation + invalidation on use.
Refs: #412
```

```txt
fix(api): handle null userId in request context

Some requests arrive without auth headers; this prevented proper 401 responses.
```

## Conventional Commits (optional policy)

If your team wants structured messages:

- `feat: ...` → feature
- `fix: ...` → bugfix
- `docs: ...`, `refactor: ...`, `test: ...`, `chore: ...`

Example:

```txt
refactor(parser): simplify tokenization
```

## Practical rules

- Keep the subject line:
  - short (often <= 50–72 chars)
  - in **imperative** mood (“Add”, “Fix”, “Remove”, “Refactor”)
  - no trailing period
- Use the body to explain:
  - motivation (“why”)
  - constraints/tradeoffs
  - user-visible behavior changes
- Reference issues/PRs when relevant
- Avoid:
  - “WIP”, “fix”, “stuff”, “changes”
  - bundling multiple unrelated changes in one commit

## When to amend

- Fix typos in the last message
- Add a missing change to the last commit (private branch)

```bash
git commit --amend
```

If already pushed/shared, coordinate before rewriting history (see [[git-rebase]] and [[git-push]] with `--force-with-lease`).

## Related notes

- [[BestPractices/CommitStrategies/AtomicCommits|Atomic Commits]]
- [[BestPractices/CommitStrategies/CommitMessageTemplates|Commit Message Templates]]
- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]
