---
id: git-write-tree
aliases: []
tags: []
---

# git write-tree

Create a tree object from the current index (staging area).

## Syntax

```bash
git write-tree
```

## Description

`git write-tree` takes the current contents of the index (the [[StagingArea]]) and writes a _tree object_ representing that directory snapshot.

- It does **not** create a commit.
- It does **not** update branches.
- It outputs the tree’s object ID.

This command is foundational for understanding Git’s internal model: commits point to trees, trees point to blobs/trees.

Related concepts:

- [[StagingArea]]
- [[GitObjects]]
- [[Commit]]

## Basic Usage

### Write a tree for what’s staged

```bash
git status
git add .
git write-tree
# outputs: <tree-hash>
```

### Inspect the resulting tree

```bash
tree_hash=$(git write-tree)
git cat-file -p "$tree_hash"
```

## Typical Plumbing Flow (High Level)

1. Stage files (`git add …`)
2. Write tree (`git write-tree`) → tree hash
3. Create commit (`git commit-tree …`) → commit hash
4. Move branch ref (`git update-ref …`) to that commit

## Troubleshooting

### “Nothing staged / unexpected tree”

`git write-tree` reflects the **index**, not your working directory. Verify:

```bash
git diff           # unstaged
git diff --staged  # staged
```

## Related Commands

- [[git-add]] - populate the index
- [[git-cat-file]] - inspect tree objects
- [[git-commit-tree]] - create a commit from a tree
- [[GitObjects]]
