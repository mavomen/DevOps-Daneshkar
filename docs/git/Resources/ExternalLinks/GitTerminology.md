---
id: GitTerminology
aliases: []
tags: []
---

# Git Terminology (Glossary)

Core Git terms used throughout the vault.

## Repository (repo)

A database of Git objects + refs. Usually a folder containing a `.git/` directory.

## Working tree (working directory)

Your checked-out files on disk (what you edit).

## Staging area (index)

A “planned snapshot” of what will go into the next commit.

See: [[StagingArea]]

## Commit

A snapshot of the project plus metadata; points to a tree and parent commit(s).

See: [[Commit]]

## Branch

A movable pointer (ref) to a commit (e.g., `main`, `feature/x`).

See: [[Branch]]

## Tag

A named pointer to a commit (often a release). Annotated tags store metadata.

See: [[git-tag]]

## HEAD

A pointer describing your current checkout (usually points to a branch ref; sometimes directly to a commit).

See: [[HEAD]]

## Detached HEAD

When `HEAD` points directly to a commit (not a branch). New commits won’t move a branch unless you create one.

See: [[DetachedHead|DetachedHead]]

## Remote

A named reference to another repository (e.g., `origin`). Used for fetch/push.

See: [[Remote]], [[git-remote]]

## origin

A conventional default remote name created on clone.

See: [[UpstreamAndOrigin]]

## upstream

Often either:

- a remote named `upstream` (fork workflow), and/or
- the tracked upstream branch (e.g., `main` tracks `origin/main`)

See: [[UpstreamAndOrigin]]

## Remote-tracking branch

A local ref that tracks a remote branch (e.g., `origin/main`). Updated by `fetch`.

## Fetch / Pull / Push

- **fetch**: download new objects + update remote-tracking refs (no integration)
- **pull**: fetch + integrate (merge/rebase depending on config)
- **push**: send commits/refs to a remote

See: [[git-fetch]], [[git-pull]], [[git-push]]

## Merge

Integrate histories by combining two branches (may create a merge commit).

See: [[git-merge]]

## Rebase

Reapply commits onto a new base commit, rewriting commit hashes.

See: [[git-rebase]]

## Fast-forward

A merge that just moves a branch pointer forward because there’s no divergence.

## Conflict

Git can’t auto-merge; you must resolve manually.

See: [[ConflictResolution]]

## Reflog

Local log of where refs (especially `HEAD`) pointed in the past. Great for recovery.

See: [[git-reflog]]

## Bisect

Binary search over history to find the commit that introduced a bug.

See: [[git-bisect]]
