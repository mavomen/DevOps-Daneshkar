---
id: Remote
aliases: []
tags: []
---

# Remote

A remote is a reference to a Git repository hosted on an external server, enabling collaboration by sharing commits between different repositories.

## What is a Remote?

A remote represents:

- A Git repository on another server (GitHub, GitLab, etc.)
- A way to share code with others
- Backup storage for your local repository
- Central coordination point for teams

## Remote Concepts

### Remote vs Local

- **Local Repository**: On your machine, complete with history
- **Remote Repository**: On external server, shared with team
- **Clone**: Local copy of remote repository
- **Sync**: Keeping local and remote in sync

### Common Remote Names

- **origin**: Default remote name for cloned repositories
- **upstream**: Original repository when working with forks
- **fork**: Your personal copy of someone else's repository

## Working with Remotes

### Adding Remotes

```bash
# Add remote repository
git remote add origin https://github.com/user/repo.git

# Add additional remote
git remote add upstream https://github.com/original/repo.git

# Add with SSH
git remote add origin git@github.com:user/repo.git
```

### Viewing Remotes

```bash
# List remotes
git remote

# List remotes with URLs
git remote -v

# Show detailed remote info
git remote show origin

# Check remote URL
git remote get-url origin
```

### Modifying Remotes

```bash
# Change remote URL
git remote set-url origin https://github.com/user/new-repo.git

# Rename remote
git remote rename origin upstream

# Remove remote
git remote remove old-remote
```

## Remote Operations

### Fetching from Remote

```bash
# Download latest changes (no merge)
git fetch origin

# Fetch all remotes
git fetch --all

# Fetch specific branch
git fetch origin feature-branch

# Fetch tags
git fetch --tags
```

### Pulling from Remote

```bash
# Fetch and merge
git pull origin main

# Fetch and rebase
git pull --rebase origin main

# Pull current branch from its tracking remote
git pull
```

### Pushing to Remote

```bash
# Push to specific remote and branch
git push origin main

# Push and set upstream tracking
git push -u origin feature-branch

# Push all branches
git push origin --all

# Push tags
git push origin --tags

# Force push (dangerous)
git push --force origin feature-branch

# Safer force push
git push --force-with-lease origin feature-branch
```

## Remote Tracking

### Upstream Branches

```bash
# Set upstream for current branch
git branch --set-upstream-to=origin/main

# Push and set upstream
git push -u origin feature-branch

# Check tracking relationships
git branch -vv

# See remote tracking status
git status -sb
```

### Tracking Information

```bash
# See which remote branches are tracked
git branch -r

# See local branches and their remotes
git branch -vv

# Check ahead/behind status
git status
```

## Remote Workflows

### Basic Collaboration

```mermaid
graph LR
    A[Local Repo] -->|push| B[Remote Repo]
    B -->|fetch/pull| C[Teammate's Repo]
    C -->|push| B
    B -->|fetch/pull| A
```

### Fork Workflow

```mermaid
graph TD
    A[Original Repo] -->|fork| B[Your Fork]
    B -->|clone| C[Local Repo]
    C -->|push| B
    B -->|Pull Request| A
```

### Team Development Flow

```bash
# Start work day
git switch main
git pull origin main

# Create feature branch
git switch -c feature/new-feature

# Work and commit
git add .
git commit -m "Implement feature"

# Push feature branch
git push -u origin feature/new-feature

# Create pull request
# After review and merge, clean up
git switch main
git pull origin main
git branch -d feature/new-feature
```

## Remote Branch Management

### Remote Branch Operations

```bash
# List remote branches
git branch -r

# Create local branch tracking remote
git switch -c local-branch origin/remote-branch

# Delete remote branch
git push origin --delete old-branch

# Prune deleted remote branches
git remote prune origin

# Update remote tracking info
git remote update origin --prune
```

### Branch Synchronization

```bash
# Update local branch from remote
git pull origin main

# Push local changes to remote
git push origin feature-branch

# Handle diverged branches
git pull --rebase origin main
git push origin main
```

## Related Notes

- [[RemoteServicesAndAuth]] — Extended coverage
