---
id: ConceptDefinitions
aliases: []
tags: []
---

# Concept Definitions

Short definitions for key concepts used across the vault.

## Porcelain vs Plumbing

- **Porcelain**: user-friendly commands (e.g., `git status`, `git commit`)
- **Plumbing**: low-level commands used internally or in scripts (e.g., `git cat-file`, `git write-tree`)

See: [[git-cat-file]], [[git-write-tree]]

## Snapshot model

Git stores snapshots (trees/blobs) of content, not diffs as primary storage (though deltas may be used internally in packfiles).

## DAG (Directed Acyclic Graph)

Commit history forms a DAG:

- nodes: commits
- edges: parent pointers

This explains merges (multiple parents) and why `rebase` rewrites ancestry.

## Three-way merge

A merge that uses:

- common ancestor (merge base)
- “ours”
- “theirs”

See: [[ThreeWayMerge]] and [[ConflictResolution]]

## “Ours” vs “Theirs”

Meaning depends on operation context (merge vs rebase), but in a merge:

- ours = current branch
- theirs = the branch being merged in

See: [[ConflictResolution]]

## Upstream tracking

A local branch can track a remote-tracking branch (e.g., `main` tracks `origin/main`), enabling `git pull`/`git push` defaults.

See: [[UpstreamAndOrigin]]

## Fast-forward vs merge commit

- fast-forward: just moves branch pointer forward
- merge commit: a new commit with two parents, preserving branch topology

## History rewriting

Operations that create new commits (new hashes) to represent existing changes:

- rebase
- reset (when followed by new commits)
- filter-branch

See: [[git-rebase]], [[git-reset]], [[git-filter-branch]]

## Safe undo vs destructive undo

- safe undo: add new commit to negate changes (`git revert`)
- destructive undo: move refs and possibly discard changes (`git reset --hard`)

See: [[git-revert]] and [[git-reset]]
