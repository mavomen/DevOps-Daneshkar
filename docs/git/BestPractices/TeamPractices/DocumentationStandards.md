---
id: DocumentationStandards
aliases: []
tags: []
---

# Documentation Standards

Documentation is part of the product. Set a standard so docs stay useful and current.

## What to document (minimum)

- how to run locally
- how to test
- configuration and environment variables
- deployment/release process
- architecture overview (if non-trivial)

## Where docs live

- `README.md`: quick start + overview
- `docs/`: deeper docs (architecture, runbooks)
- PR descriptions: change context and test plan

Template: [[ProjectReadmeTemplate]]

## Style guidelines

- write for the next developer (often “future you”)
- keep headings consistent
- include copy-paste commands
- show examples (inputs/outputs)
- avoid outdated “TODO” sections

## Updating docs with code changes

- docs should change in the same PR as the behavior change
- reviewers should treat docs drift as a real issue

## Related Notes

- [[RepositoryStructure]]
- [[PullRequestTemplate]]
- [[Workflows/CodeReviewWorkflow|Code Review Workflow]]
