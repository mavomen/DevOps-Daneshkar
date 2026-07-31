---
id: LongRunningBranches
aliases: []
tags: []
---

# Long-Running Branches

Long-running branches (like `main`, `develop`, `release/*`) exist for extended periods and anchor your workflow.

## When they make sense

- you need stabilization windows (release branches)
- you separate integration from production (Git Flow: `develop` vs `main`)
- you ship multiple supported versions concurrently

Related:

- [[Workflows/GitFlowWorkflow|Git Flow Workflow]]
- [[Workflows/ReleaseWorkflow|Release Workflow]]
- [[Workflows/HotfixWorkflow|Hotfix Workflow]]

## Risks

- increased merge conflicts due to divergence
- “drift” between production and integration branches
- confusing ownership (“which branch is truth?”)

## Best practices

- keep the number of long-running branches minimal
- define clear semantics:
  - `main` = production-ready
  - `develop` = next release integration
- enforce protections (see [[BestPractices/BranchingStrategies/BranchProtectionRules|Branch Protection Rules]])
- integrate frequently:
  - merge hotfixes back to integration branches
  - regularly sync `develop` with `main` as policy dictates

## Practical patterns

### Hotfix propagation

After merging a hotfix to `main`, propagate to `develop`:

- merge or cherry-pick (policy dependent)

See: [[Workflows/HotfixWorkflow|Hotfix Workflow]] and [[git-cherry-pick]].

### Release branch hygiene

- allow only bugfixes/docs/version bumps
- tag releases from `main` (or the release branch if your policy says so)
- delete release branches after completion

## Related notes

- [[BestPractices/BranchingStrategies/BranchLifecycle|Branch Lifecycle]]
- [[UpstreamAndOrigin]]
