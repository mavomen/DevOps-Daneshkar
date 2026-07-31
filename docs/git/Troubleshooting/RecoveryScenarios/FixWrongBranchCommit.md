---
id: FixWrongBranchCommit
aliases: []
tags: []
---

# Fix Wrong Branch Commit

You committed to the wrong branch and want the commit on a different branch.

## Scenario 1: Commit not pushed (cleanest)

1. On the wrong branch, undo commit but keep changes staged:

```bash
git reset --soft HEAD~1
```

2. Switch to correct branch and commit:

```bash
git switch <correct-branch>
git commit -m "Correct commit message"
```

## Scenario 2: Commit already exists and you want to move it via cherry-pick

1. Note the commit hash:

```bash
git log --oneline -n 5
```

2. On correct branch, cherry-pick it:

```bash
git switch <correct-branch>
git cherry-pick <commit-hash>
```

3. Remove it from wrong branch:

- if not pushed: `git reset --hard HEAD~1`
- if pushed/shared: `git revert <commit-hash>`

## Related Notes

- [[git-reset]]
- [[git-cherry-pick]]
- [[git-revert]]
