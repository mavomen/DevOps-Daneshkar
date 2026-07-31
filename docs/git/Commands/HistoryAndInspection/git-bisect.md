---
id: git-bisect
aliases: []
tags: []
---

# git bisect

Use binary search to find the commit that introduced a bug.

## Syntax

```bash
git bisect start
git bisect good <commit>
git bisect bad <commit>
git bisect reset

# Optional automation
git bisect run <command>...
```

## Description

`git bisect` helps you locate the first bad commit by repeatedly checking out a midpoint commit between a known “good” state and a known “bad” state.

This turns “check N commits” into about “check log2(N) commits”.

## Basic Usage (Manual)

### 1) Start

```bash
git bisect start
```

### 2) Mark a bad commit (often HEAD)

```bash
git bisect bad HEAD
```

### 3) Mark a good commit (a known good tag/sha)

```bash
git bisect good v1.0.0
# or
git bisect good <commit-hash>
```

### 4) Test the checked-out revision

Git will checkout a commit for you. You then test the behavior.

- If bug exists:

```bash
git bisect bad
```

- If bug does not exist:

```bash
git bisect good
```

Repeat until Git prints the first bad commit.

### 5) Exit bisect mode

```bash
git bisect reset
```

## Automated Bisect (`git bisect run`)

If you can express “good vs bad” as a script/command exit code:

- exit `0` = good
- exit `1..127` (except `125`) = bad
- exit `125` = skip (can’t test this commit)

Example:

```bash
git bisect start
git bisect bad HEAD
git bisect good v1.0.0
git bisect run ./run-tests.sh
git bisect reset
```

## Skipping Commits

If a particular revision can’t be tested (won’t build, etc.):

```bash
git bisect skip
```

Or skip a range:

```bash
git bisect skip <commit> <commit>
```

## Common Workflow

```bash
# pick a known good release tag and current bad HEAD
git bisect start
git bisect bad HEAD
git bisect good v1.2.0

# now test each checkout
# ...
git bisect reset
```

After you find the bad commit:

- inspect it: [[git-show]]
- revert it: [[git-revert]]
- or create a fix commit

## Troubleshooting

### You ended bisect on a detached state

That’s normal during bisect. Always exit with:

```bash
git bisect reset
```

### Your test command is flaky

- Make the test deterministic
- Avoid network dependencies
- Prefer unit/integration tests over manual checks

## Related Commands

- [[git-log]] - pick good/bad boundaries
- [[git-show]] - inspect candidate commits
- [[git-blame]] - map broken lines to commits
- [[git-revert]] - undo a bad commit safely
