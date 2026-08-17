---
id: git-filter-branch
aliases: []
tags: []
---

# git filter-branch

Rewrite Git history by filtering commits (e.g., remove a file from all commits).

## Syntax

```bash
git filter-branch [<options>] [<revision-list>]
```

## Description

`git filter-branch` is a powerful history-rewriting command. Common use-cases:

- remove secrets accidentally committed (keys, tokens)
- delete large files from history
- rewrite author info
- move paths around historically

This rewrites commits, producing new commits with new [[SHAHash]] values.

> Warning: rewriting history that’s already shared can disrupt collaborators. Prefer doing this only with coordination and clear communication.

## Basic Usage (Typical Secret Removal Pattern)

Example: remove a tracked file from all history:

```bash
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch path/to/secret.txt" \
  --prune-empty --tag-name-filter cat -- --all
```

After this, you typically need to force-push branches/tags (team coordination required):

```bash
git push --force --all
git push --force --tags
```

## Options (Common)

### Rewrite authors

```bash
git filter-branch --env-filter '
if [ "$GIT_AUTHOR_EMAIL" = "old@example.com" ]; then
  GIT_AUTHOR_NAME="New Name"
  GIT_AUTHOR_EMAIL="new@example.com"
  GIT_COMMITTER_NAME="New Name"
  GIT_COMMITTER_EMAIL="new@example.com"
fi
' -- --all
```

## Troubleshooting

### “I need to undo filter-branch”

- Create backups before running.
- If you ran it recently, check:

```bash
git reflog
```

And restore old refs if available (advanced). Safer is: keep a backup clone before rewriting.

### “We already pushed the bad history”

- Rewriting is still possible but requires:
  - force-push coordination
  - everyone to re-clone or hard reset to new history
- Also rotate any leaked secrets regardless of cleanup.

## Related Notes

- [[git-rebase]] - rewrite a small recent range (safer for day-to-day)
- [[git-reflog]] - recovery when history manipulation goes wrong
- [[git-push]] - force-push after history rewrite (with care)
