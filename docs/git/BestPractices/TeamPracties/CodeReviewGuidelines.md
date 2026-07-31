---
id: CodeReviewGuidelines
aliases: []
tags: []
---

# Code Review Guidelines

Code review is a quality gate and a knowledge-sharing mechanism. The goal is correctness, maintainability, and shared ownership—not “winning arguments”.

## What reviewers should look for

### Correctness

- does it meet requirements?
- edge cases and error paths
- data validation and security concerns

### Maintainability

- clarity and readability
- reasonable naming and structure
- unnecessary complexity removed

### Testing

- tests added/updated for behavior
- meaningful test coverage (not only “happy path”)
- deterministic tests (avoid flaky dependencies)

### Performance (when relevant)

- obvious inefficiencies
- scalability concerns
- safe defaults

## PR size guidelines

- Keep PRs small enough to review in one sitting.
- If a change is large, split into:
  - preparatory refactor PR
  - feature PR
  - follow-up cleanups

See: [[AtomicCommits]]

## PR description checklist

Include:

- summary (what)
- motivation (why)
- how to test
- screenshots (if UI)
- risk/rollout notes

Template: [[PullRequestTemplate]]

## Review etiquette (team health)

- be specific: point to line, behavior, consequence
- separate “must fix” from “nice to have”
- assume good intent
- prefer suggestions with examples

## Related Notes

- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]
- [[BranchProtectionRules]]
- [[CommitMessageBestPractices]]
