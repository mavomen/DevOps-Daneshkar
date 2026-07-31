---
id: 01-FundamentalsMOC
aliases: []
tags: []
---

# Fundamentals (MOC)

Git’s basic model: files change in the working directory, get staged, then committed into history.

## Concepts

- [[Concepts/VersionControl|What is Version Control]]
- [[Concepts/Repository|Repository]]
- [[WorkingDirectory|WorkingDirectory]]
- [[StagingArea|StagingArea]]
- [[TheThreeStates|TheThreeStates]]
- [[FileLifecycle|FileLifecycle]]
- [[Concepts/Commit|Commit]]
- [[SHAHash|SHAHash]]
- [[GitHistory|GitHistory]]
- [[Concepts/HEAD|HEAD]]

## Commands (the fundamentals loop)

1. Inspect
   - [[Commands/BasicOperations/git-status|git status]]
   - [[Commands/BasicOperations/git-diff|git diff]]
2. Stage
   - [[Commands/Setup/git-add|git add]]
3. Commit
   - [[Commands/BasicOperations/git-commit|git commit]]
4. Verify history
   - [[Commands/BasicOperations/git-log|git log]]
   - [[Commands/BasicOperations/git-show|git show]]

## Minimal daily loop

1. `git status`
2. edit files
3. `git diff`
4. `git add`
5. `git diff --staged`
6. `git commit`
7. `git log --oneline`
