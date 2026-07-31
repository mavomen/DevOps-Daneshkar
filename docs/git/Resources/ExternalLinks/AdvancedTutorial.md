---
id: AdvancedTutorial
aliases: []
tags: []
---

# Advanced Tutorials

Deep dives for when you already understand daily Git usage.

## Advanced Git topics

- Git internals / objects (start here): https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain
- `git bisect` docs: https://git-scm.com/docs/git-bisect
- `git reflog` docs: https://git-scm.com/docs/git-reflog
- `git worktree` docs: https://git-scm.com/docs/git-worktree
- `git submodule` docs: https://git-scm.com/docs/git-submodule
- `git filter-branch` docs (history rewriting): https://git-scm.com/docs/git-filter-branch

## Suggested learning path (advanced)

1. Understand object types:
   - commit / tree / blob / tag
2. Learn safe recovery patterns:
   - reflog-based recovery
3. Learn selective history tools:
   - cherry-pick, interactive rebase
4. Learn advanced repo layouts:
   - worktrees, submodules (only if you need them)

## Map to vault notes

- Plumbing:
  - [[git-cat-file]]
  - [[git-hash-object]]
  - [[git-write-tree]]
  - [[git-commit-tree]]
  - [[git-update-ref]]
  - [[git-rev-parse]]
- Advanced operations:
  - [[git-cherry-pick]]
  - [[git-worktree]]
  - [[git-submodule]]
  - [[git-filter-branch]]
- Debugging:
  - [[git-bisect]]
  - [[git-blame]]
  - [[git-reflog]]

## Related Notes

- [[BestPractices/RepositoryManagement/LargeRepositoryHandling|Large Repository Handling]]
- [[BestPractices/RepositoryManagement/SecurityPractices|Security Practices]]
