---
id: git-commit-tree
aliases: []
tags: []
---

# git commit-tree

Create a commit object from a tree object (and optional parent commit(s)).

## Syntax

```bash
git commit-tree <tree> [-p <parent> ...] [-m <message>]
```

## Description

`git commit-tree` creates a commit object directly (plumbing).

- You provide:
  - a tree hash (snapshot)
  - zero or more parents (to form history)
  - a commit message
- It outputs the new commit hash.
- It does **not** move any branch ref by itself.

This is a low-level equivalent of what `git commit` ultimately does, but without the friendly workflow.

Related concepts:

- [[Commit]]
- [[GitObjects]]
- [[HEAD]]

## Basic Usage

### Create a commit from the current index

```bash
# stage what you want
git add .

# create a tree from index
tree_hash=$(git write-tree)

# create a commit object
commit_hash=$(echo "My plumbing commit" | git commit-tree "$tree_hash")
echo "$commit_hash"
```

### Create a commit with a parent (normal history)

```bash
git add .
tree_hash=$(git write-tree)

parent=$(git rev-parse HEAD)
commit_hash=$(echo "Commit with parent" | git commit-tree "$tree_hash" -p "$parent")
echo "$commit_hash"
```

### Create a merge commit (two parents)

```bash
tree_hash=$(git write-tree)
p1=$(git rev-parse main)
p2=$(git rev-parse feature/branch)

commit_hash=$(echo "Merge commit (plumbing)" | git commit-tree "$tree_hash" -p "$p1" -p "$p2")
echo "$commit_hash"
```

## After Creating the Commit: Update a Ref

To make this commit reachable (e.g., move `refs/heads/main`):

```bash
git update-ref refs/heads/main "$commit_hash"
```

> Be careful: this can rewrite history.

## Troubleshooting

### Wrong author/committer info

`git commit-tree` uses environment variables for identity/time (like normal Git). Check:

```bash
git config user.name
git config user.email
```

And environment variables if you set them in your shell.

## Related Commands

- [[git-write-tree]] - create the tree snapshot
- [[git-update-ref]] - move branch refs to your new commit
- [[git-rev-parse]] - resolve refs/hashes
- [[git-cat-file]] - inspect the commit you created
