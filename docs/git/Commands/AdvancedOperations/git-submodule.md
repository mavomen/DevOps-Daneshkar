---
id: git-submodule
aliases: []
tags: []
---

# git submodule

Include one Git repository inside another as a subdirectory, while keeping histories separate.

## Syntax

```bash
git submodule add <url> [<path>]
git submodule init
git submodule update
git submodule update --init --recursive
git submodule status
```

## Description

A submodule pins a specific commit of another repository inside your repo. This is useful when you want to vendor a dependency but still keep it as an independent repo.

Key points:

- The parent repo tracks a _specific commit_ of the submodule
- Cloning requires extra steps (or `--recurse-submodules`)
- Updating requires explicit submodule commands

## Basic Usage

### Add a submodule

```bash
git submodule add https://github.com/some/lib.git libs/lib
```

This creates/updates:

- `.gitmodules`
- the submodule directory entry in the index

### Clone a repo with submodules

```bash
git clone --recurse-submodules <url>
```

If you already cloned without recursion:

```bash
git submodule update --init --recursive
```

### Check status

```bash
git submodule status
```

## Common Workflows

### Update submodule to latest commit on its default branch

Inside the submodule directory:

```bash
cd libs/lib
git fetch
git switch main
git pull --ff-only
```

Back in the parent repo:

```bash
cd ../..
git status
git add libs/lib
git commit -m "Update submodule libs/lib"
```

## Troubleshooting

### “Submodule directory is empty after clone”

Run:

```bash
git submodule update --init --recursive
```

### Detached HEAD inside submodule

That’s normal: submodules often checkout a specific commit. If you want to work on it, create a branch inside the submodule.

## Related Commands

- [[git-clone]] - use `--recurse-submodules`
- [[git-fetch]] / [[git-pull]] - used inside submodule repos
- [[git-worktree]] - sometimes a better alternative for local multi-repo work
