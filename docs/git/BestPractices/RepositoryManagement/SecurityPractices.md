---
id: SecurityPractices
aliases: []
tags: []
---

# Security Practices

Git hygiene intersects with security: secrets handling, access control, review discipline, and safe history operations.

## Core principles

- never commit secrets
- assume anything committed may become visible (now or later)
- protect critical branches
- keep auditability (prefer `revert` over history rewrites on shared branches)

Related:

- [[GitIgnorePatterns]]
- [[GitHooks]]
- [[BestPractices/BranchingStrategies/BranchProtectionRules|Branch Protection Rules]]
- [[git-revert]]
- [[git-filter-branch]]

## Secrets handling

### Prevent

- add `.env`, keys, credentials to `.gitignore`
- add pre-commit checks (hooks) to block common secret patterns
- use secret managers / CI variables instead of repo files

See: [[GitIgnorePatterns]], [[GitHooks]]

### If a secret was committed

1. Rotate/revoke the secret immediately (always)
2. Decide remediation:
   - if not pushed/shared: you may fix locally (rewrite)
   - if pushed/shared: coordinate; consider history rewrite + force push (complex)

History rewrite options are dangerous but sometimes necessary:

- see [[git-filter-branch]]
- use [[git-reflog]] for local recovery if mistakes occur

## Access control and collaboration

- protect `main`/release branches (PR-only)
- require CI checks and approvals
- limit who can push or approve (policy-based)

See: [[BestPractices/BranchingStrategies/BranchProtectionRules|Branch Protection Rules]]

## Safe defaults

- avoid `git push --force` on shared branches
- prefer `--force-with-lease` when rewriting a private feature branch
- use `git revert` for undo on shared branches

Related commands:

- [[git-push]]
- [[git-revert]]
- [[git-reset]]

## Related notes

- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]
- [[CiCdIntegration]]
