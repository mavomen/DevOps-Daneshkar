---
id: git-remote
aliases: []
tags: []
---

# git remote

Manage remote repositories (list, add, rename, remove, inspect URLs).

## Syntax

```bash
git remote
git remote -v
git remote add <name> <url>
git remote remove <name>
git remote rename <old> <new>
git remote set-url <name> <newurl>
git remote show <name>
```

## Description

The `git remote` command manages named references to other [[Concepts/Repository|repositories]] (usually hosted on GitHub/GitLab). A remote name (commonly `origin`) maps to one or more URLs used for fetching and pushing.

A remote is not “special” in Git itself—it's just a named pointer. Team conventions often treat:

- `origin` as “the repo you cloned from”
- `upstream` as “the canonical repo” (when you work from a fork)

See: [[Concepts/Remote|Remote]]

## Basic Usage

### List Remotes

```bash
# List remote names
git remote

# List remote names with URLs (fetch/push)
git remote -v
```

### Add a Remote

```bash
# Add origin
git remote add origin https://github.com/user/repo.git

# Add upstream (common in fork workflows)
git remote add upstream https://github.com/original/repo.git
```

### Rename / Remove

```bash
# Rename a remote
git remote rename origin upstream

# Remove a remote
git remote remove upstream
```

## URLs

### Get/Set URL

```bash
# Show remote URL (fetch)
git remote get-url origin

# Show push URL (may differ)
git remote get-url --push origin

# Change remote URL
git remote set-url origin https://github.com/user/new-repo.git

# Set a different push URL (optional advanced)
git remote set-url --push origin git@github.com:user/repo.git
```

## Inspect Remote

```bash
# Show remote details (tracked branches, HEAD branch, etc.)
git remote show origin
```

## Remote Cleanup (Pruning)

```bash
# Remove stale remote-tracking branches that were deleted on server
git remote prune origin

# Preview prune
git remote prune origin --dry-run
```

## Common Workflows

### Fork Setup (origin + upstream)

```bash
# You cloned your fork
git remote -v

# Add canonical project as upstream
git remote add upstream https://github.com/original/repo.git

# Fetch upstream and update your main
git fetch upstream
git switch main
git merge upstream/main
git push origin main
```

### Changing HTTPS ↔ SSH

```bash
# Switch origin to SSH (after setting up SSH keys)
git remote set-url origin git@github.com:user/repo.git
```

## Troubleshooting

### “remote origin already exists”

```bash
git remote -v
# Either remove or set-url
git remote set-url origin <url>
```

### “Repository not found” / auth problems

- Verify URL: `git remote -v`
- Check whether you have access (private repos need auth)
- Prefer SSH for fewer credential prompts (if configured)

## Related Commands

- [[Commands/Remote/git-fetch|git fetch]] - Download refs/objects from remote
- [[Commands/Remote/git-pull|git pull]] - Fetch + integrate into current branch
- [[Commands/Remote/git-push|git push]] - Upload commits/refs to remote
- [[Commands/Setup/git-clone|git clone]] - Create local copy + set default remote
