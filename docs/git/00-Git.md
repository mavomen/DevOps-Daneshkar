---
id: 00-Git
aliases: []
tags: []
---

# Git Overview (MOC)

This is the canonical entry point for the Git vault (concepts → commands → workflows → troubleshooting → internals).

## Start Here

1. [[01-FundamentalsMoc|01 Fundamentals (MOC)]]
2. [[02-DailyWorkflowMoc|02 Daily Workflow (MOC)]]
3. [[03-AdvancedFeaturesMoc|03 Advanced Features (MOC)]]
4. [[04-CollaborationMoc|04 Collaboration (MOC)]]
5. [[05-TroubleshootingMoc|05 Troubleshooting (MOC)]]
6. [[06-Internals|06 Internals & Advanced (MOC)]]

## Concepts (Core)

- [[Concepts/VersionControl|What is Version Control]]
- [[DistributedvsCentralized|Distributed vs Centralized]]
- [[DistributedMigration|Distributed Migration]]
- [[Concepts/Repository|Repository]]
- [[WorkingDirectory|Working Directory]]
- [[WorkingDirectoryPatterns|Working Directory Patterns]]
- [[StagingArea|Staging Area]]
- [[StagingAreaAdvanced|Staging Area Advanced]]
- [[TheThreeStates|The Three States]]
- [[StateTransitionsAndPatterns|State Transitions & Patterns]]
- [[FileLifecycle|File Lifecycle]]
- [[FileTrackingAndOperations|File Tracking & Operations]]

## Concepts (History & Identity)

- [[Concepts/Commit|Commit]]
- [[CommitOperationsAndAdvanced|Commit Operations & Advanced]]
- [[GitHistory|Git History]]
- [[GitHistoryManagement|Git History Management]]
- [[SHAHash|SHA Hash]]
- [[SHAHashTypesAndSecurity|SHA Hash Types & Security]]
- [[Concepts/HEAD|HEAD]]
- [[HEADInternalsAndPractical|HEAD Internals & Practical]]

## Concepts (Branching & Integration)

- [[Concepts/Branch|Branch]]
- [[BranchManagement|Branch Management]]
- [[MergevsRebase|Merge vs Rebase]]
- [[MergevsRebaseWorkflows|Merge vs Rebase Workflows]]
- [[ThreeWayMerge|Three-Way Merge]]
- [[MergeConflictResolution|Merge Conflict Resolution]]
- [[FastForwardMerge|Fast-Forward Merge]]
- [[InteractiveRebase|Interactive Rebase]]
- [[SquashingCommits|Squashing Commits]]
- [[ConflictResolution|Conflict Resolution]]

## Concepts (Remote)

- [[Concepts/Remote|Remote]]
- [[RemoteServicesAndAuth|Remote Services & Auth]]
- [[UpstreamAndOrigin|Upstream & Origin]]
- [[CollaborationStrategies|Collaboration Strategies]]

## Concepts (Internals)

- [[GitObjects|Git Objects]]
- [[GitObjectManagement|Git Object Management]]

## Commands (Setup)

- [[Commands/Setup/git-init|git init]]
- [[Commands/BasicOperations/git-clone|git clone]]
- [[Commands/BasicOperations/git-add|git add]]
- [[Commands/Setup/git-config|git config]]

## Commands (Basic Operations)

- [[Commands/BasicOperations/git-status|git status]]
- [[Commands/BasicOperations/git-diff|git diff]]
- [[Commands/BasicOperations/git-commit|git commit]]
- [[Commands/BasicOperations/git-log|git log]]
- [[Commands/BasicOperations/git-show|git show]]
- [[Commands/BasicOperations/git-restore|git restore]]
- [[Commands/BasicOperations/git-rm|git rm]]

## Commands (Branching)

- [[Commands/Branching/git-branch|git branch]]
- [[Commands/Branching/git-switch|git switch]]
- [[Commands/Branching/git-checkout|git checkout]]
- [[Commands/Branching/git-merge|git merge]]
- [[Commands/Branching/git-rebase|git rebase]]

## Commands (Remote)

- [[Commands/Remote/git-remote|git remote]]
- [[Commands/Remote/git-fetch|git fetch]]
- [[Commands/Remote/git-pull|git pull]]
- [[Commands/Remote/git-push|git push]]

## Commands (Advanced Operations)

- [[Commands/AdvancedOperations/git-stash|git stash]]
- [[Commands/AdvancedOperations/git-cherry-pick|git cherry-pick]]
- [[Commands/AdvancedOperations/git-tag|git tag]]
- [[Commands/AdvancedOperations/git-worktree|git worktree]]

## Commands (Plumbing)

- [[Commands/Plumbing/git-cat-file|git cat-file]]
- [[Commands/Plumbing/git-hash-object|git hash-object]]
- [[Commands/Plumbing/git-ls-tree|git ls-tree]]
- [[Commands/Plumbing/git-rev-parse|git rev-parse]]
- [[Commands/Plumbing/git-commit-tree|git commit-tree]]
- [[Commands/Plumbing/git-update-ref|git update-ref]]
- [[Commands/Plumbing/git-write-tree|git write-tree]]

## Commands (Patch)

- [[Commands/Patch/git-apply|git apply]]
- [[Commands/Patch/git-am|git am]]
- [[Commands/Patch/git-format-patch|git format-patch]]

## Commands (Utilities)

- [[Commands/Utilities/git-bisect|git bisect]]
- [[Commands/Utilities/git-blame|git blame]]
- [[Commands/Utilities/git-clean|git clean]]
- [[Commands/Utilities/git-check-ignore|git check-ignore]]
- [[Commands/Utilities/git-filter-branch|git filter-branch]]
- [[Commands/Utilities/git-fsck|git fsck]]
- [[Commands/Utilities/git-gc|git gc]]
- [[Commands/Utilities/git-shortlog|git shortlog]]
- [[Commands/Utilities/git-submodule|git submodule]]

## Configuration

- [[GitConfiguration|Git Configuration]]
- [[GitAliases|Git Aliases]]
- [[GitHooks|Git Hooks]]
- [[GitInstallation|Git Installation]]
- [[SshKeysSetup|SSH Keys Setup]]
- [[GitIgnorePatterns|Git Ignore Patterns]]
- [[GitAttributes|Git Attributes]]
- [[CiCdIntegration|CI/CD Integration]]
- [[ShellIntegration|Shell Integration]]
- [[EditorIntegration|Editor Integration]]

## Workflows

- [[RepositoryInitialization|Repository Initialization]]
- [[FirstCommit|First Commit]]
- [[FeatureBranchWorkflow|Feature Branch Workflow]]
- [[ForkAndPullRequest|Fork & Pull Request]]
- [[GitFlowWorkflow|Git Flow Workflow]]
- [[GitHubFlow|GitHub Flow]]
- [[HotfixWorkflow|Hotfix Workflow]]
- [[ReleaseWorkflow|Release Workflow]]
- [[PairProgrammingWorkflow|Pair Programming Workflow]]
- [[DailySyncWorkflow|Daily Sync Workflow]]
- [[CodeReviewWorkflow|Code Review Workflow]]

## Best Practices

### Commit Strategies

- [[AtomicCommits|Atomic Commits]]
- [[CommitFrequency|Commit Frequency]]
- [[CommitMessageBestPractices|Commit Message Best Practices]]
- [[CommitMessageTemplates|Commit Message Templates]]

### Branching Strategies

- [[BranchLifecycle|Branch Lifecycle]]
- [[BranchNamingConventions|Branch Naming Conventions]]
- [[BranchProtectionRules|Branch Protection Rules]]
- [[LongRunningBranches|Long-Running Branches]]

### Team Practices

- [[CodeReviewGuidelines|Code Review Guidelines]]
- [[DocumentationStandards|Documentation Standards]]
- [[MergeVsRebaseStrategy|Merge vs Rebase Strategy]]
- [[OnboardingNewDevelopers|Onboarding New Developers]]
- [[ReleaseManagement|Release Management]]

### Repository Management

- [[LargeRepositoryHandling|Large Repository Handling]]
- [[MonorepoVsMultirepo|Monorepo vs Multirepo]]
- [[PerformanceOptimization|Performance Optimization]]
- [[RepositoryStructure|Repository Structure]]
- [[SecurityPractices|Security Practices]]

## Quick Reference

### Command Cheat Sheets

- [[DailyCommands|Daily Commands]]
- [[BranchingCommands|Branching Commands]]
- [[HistoryCommands|History Commands]]
- [[RemoteCommands|Remote Commands]]
- [[AdvancedCommands|Advanced Commands]]

### Syntax Reference

- [[BranchSyntax|Branch Syntax]]
- [[CommitSyntax|Commit Syntax]]
- [[GitIgnoreSyntax|Git Ignore Syntax]]
- [[LogFormatting|Log Formatting]]
- [[RemoteSyntax|Remote Syntax]]

### Emergency Procedures

- [[DisasterRecovery|Disaster Recovery]]
- [[EmergencyRecovery|Emergency Recovery]]
- [[QuickFixes|Quick Fixes]]
- [[RollbackProcedures|Rollback Procedures]]

## Scenarios & Exercises

- [[OpenSourceContribution|Open Source Contribution]]
- [[TeamProjectSetup|Team Project Setup]]
- [[DevOpsIntegration|DevOps Integration]]
- [[LegacyCodeIntegration|Legacy Code Integration]]
- [[ReleaseManagementProject|Release Management Project]]

## Resources

- [[OfficialDocumentation|Official Documentation]]
- [[LearningResources|Learning Resources]]
- [[CommunityResources|Community Resources]]
- [[ToolsAndExtensions|Tools & Extensions]]
- [[CommandGlossary|Command Glossary]]
- [[ConceptDefinitions|Concept Definitions]]
- [[GitTerminology|Git Terminology]]
- [[AdvancedTutorial|Advanced Tutorial]]
- [[GitWorkflowTemplate|Git Workflow Template]]
- [[CommitMessageTemplate|Commit Message Template]]
- [[PullRequestTemplate|Pull Request Template]]
- [[IssueTemplate|Issue Template]]
- [[ProjectReadmeTemplate|Project README Template]]

## Note Format

- [[NOTE_FORMAT|Note Format Guide]]
