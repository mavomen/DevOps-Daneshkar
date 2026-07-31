---
id: SquashingCommits
aliases: []
tags: []
---

# Squashing Commits

Squashing combines multiple commits into a single commit. It’s used to keep history clean (especially on `main`) while still allowing frequent commits during development.

## When to squash

- before merging a feature branch
- when your branch history contains many “fix typo”, “wip”, “address review” commits
- when team policy wants one commit per PR

## How to squash (interactive rebase)

1. Start interactive rebase:

```bash
git rebase -i HEAD~N
```

2. Change commits you want to merge into the first one:

- `pick` → keep
- `squash` → combine (keeps message)
- `fixup` → combine (drops message)

3. Save/close editor; edit final message when prompted.

See: [[InteractiveRebase]]

## Squash merge (merge without keeping commit list)

```bash
git switch main
git merge --squash feature/my-branch
git commit -m "feat: feature summary"
```

## Pros / Cons

### Pros

- cleaner history on `main`
- easier to revert a whole feature (if it’s one commit)
- easier release notes

### Cons

- loses step-by-step development context
- can hide incremental reasoning if overused

## Safety / pushing

If you squash and rewrite commits that were already pushed, you will need:

```bash
git push --force-with-lease
```

Never do this on shared branches unless explicitly coordinated.

## Related Notes

- [[git-rebase]]
- [[git-merge]]
- [[git-push]]
- [[CommitMessageBestPractices]]
