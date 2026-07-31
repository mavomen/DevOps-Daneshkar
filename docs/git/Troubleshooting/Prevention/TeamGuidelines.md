---
id: TeamGuidelines
aliases: []
tags: []
---

# Team Guidelines

A minimal set of team agreements that prevents most Git disasters.

## Recommended policies

- `main` is protected (PR only)
- CI required before merge
- merge strategy decided and documented:
  - squash vs merge commit vs rebase merge
- branch naming conventions standardized (see [[BranchNamingConventions]])
- commit message conventions standardized (see [[CommitMessageBestPractices]])

## Force push rules

- never on `main`
- allowed only on personal feature branches
- prefer `--force-with-lease`

## Secrets policy

- never commit secrets
- use secret scanning/hook checks
- rotate on incident immediately

See: [[SecurityPractices]]

## Related Notes

- [[GitWorkflowTemplate]]
- [[BranchProtectionRules]]
- [[CodeReviewWorkflow]]
