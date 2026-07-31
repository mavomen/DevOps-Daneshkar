---
id: InteractiveRebase
aliases: []
tags: []
---

# Interactive Rebase

Interactive rebase is a mode of [[git-rebase]] that lets you rewrite a sequence of commits: reorder them, edit them, squash them, or drop them.

## When to use it

Use interactive rebase on **your own feature branch** to:

- clean up “WIP” history before opening a PR
- squash tiny commits into meaningful commits
- fix commit messages (`reword`)
- split a large commit into smaller commits (`edit` + partial staging)

## When NOT to use it

Avoid rewriting history that other people already pulled.

If a branch is shared/public (especially `main`), prefer:

- rollback via [[git-revert]]
- or coordination-heavy procedures

## Core command

```bash
# edit last N commits
git rebase -i HEAD~N

# edit everything since branch diverged from main
git rebase -i main
```

## The todo list (what you’ll see)

Example:

```txt
pick a1b2c3d feat: add API endpoint
pick d4e5f6g fix: handle null userId
pick 1112223 docs: update README
```

Common actions:

- `pick` — keep commit
- `reword` — change message only
- `edit` — stop and let you amend/split
- `squash` — combine into previous commit (keeps message)
- `fixup` — combine into previous commit (drops message)
- `drop` — remove commit

## Typical workflows

### Squash commits

```bash
git rebase -i HEAD~5
# change some lines from pick -> squash/fixup
```

Then Git opens another editor to merge commit messages.

### Rename (reword) commit messages

```bash
git rebase -i HEAD~3
# change pick -> reword on the commit you want
```

### Split a commit (edit)

```bash
git rebase -i HEAD~3
# change pick -> edit on the big commit
```

Then when it stops:

```bash
git reset HEAD^
git add -p
git commit -m "Part 1"
git add -p
git commit -m "Part 2"
git rebase --continue
```

## Conflicts during interactive rebase

If conflicts happen:

```bash
git status
# fix files
git add .
git rebase --continue
```

Abort completely:

```bash
git rebase --abort
```

See: [[ConflictResolution]]

## After rebase: pushing

If you already pushed the branch, you’ll need:

```bash
git push --force-with-lease
```

## Recovery if you mess up

Use reflog:

```bash
git reflog
git reset --hard HEAD@{n}
```

See: [[git-reflog]]

## Related Notes

- [[git-rebase]]
- [[SquashingCommits]]
- [[MergevsRebase]]
- [[git-reset]]
- [[git-reflog]]
