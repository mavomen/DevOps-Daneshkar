---
id: git-update-ref
aliases: []
tags: []
---

# git update-ref

Update Git references (branches/tags) to point to a specified object ID.

## Syntax

```bash
git update-ref <ref> <newvalue> [<oldvalue>]
git update-ref -d <ref> [<oldvalue>]
```

## Description

`git update-ref` is plumbing that directly manipulates refs under `.git/refs/` (and packed-refs).

You can:

- move a branch pointer to a specific commit
- delete refs safely (optionally with an expected old value)

This is powerful and dangerous: it can rewrite history without the usual safety checks of porcelain commands.

Related concepts:

- [[Repository]]
- [[HEAD]]
- [[GitHistory]]

## Basic Usage

### Move a branch ref

```bash
# move main to a specific commit
git update-ref refs/heads/main <commit-hash>
```

### Delete a ref

```bash
git update-ref -d refs/heads/old-branch
```

## Safety Pattern: Provide the Expected Old Value

This is like a “compare-and-swap”:

```bash
git update-ref refs/heads/main <new> <old>
```

If `main` isn’t currently at `<old>`, the update fails, reducing accidental overwrites.

Example:

```bash
old=$(git rev-parse main)
new=$(git rev-parse HEAD)

git update-ref refs/heads/main "$new" "$old"
```

## Common Use Case (Plumbing Commit Flow)

```bash
git add .
tree=$(git write-tree)
parent=$(git rev-parse HEAD)
commit=$(echo "plumbing commit" | git commit-tree "$tree" -p "$parent")

git update-ref refs/heads/main "$commit"
```

## Troubleshooting / Recovery

If you moved a ref incorrectly:

- Use [[git-reflog]] to find previous positions
- Reset/move back using a known good hash

## Related Notes

- [[git-rev-parse]] - resolve refs and hashes
- [[git-reflog]] - recover previous ref positions
- [[git-commit-tree]] - create commits you might point refs to
