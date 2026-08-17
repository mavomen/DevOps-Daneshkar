---
id: Repository
aliases: []
tags: []
---

# Repository

A Git repository is a directory that contains your project files along with the complete history and metadata needed to track changes over time.

## What is a Repository?

A repository (or "repo") is the fundamental unit in Git. It's essentially a database that stores:

- All versions of your project files
- Complete change history
- Branch and tag information
- Configuration settings
- Metadata about commits, authors, and dates

## Repository Structure

```
my-project/
├── .git/                 # Git's database (hidden)
│   ├── objects/          # All file contents and commits
│   ├── refs/             # Branch and tag pointers
│   ├── HEAD              # Current branch pointer
│   ├── config            # Repository configuration
│   └── hooks/            # Automation scripts
├── src/                  # Your project files
├── docs/                 # Documentation
├── README.md             # Project description
└── .gitignore           # Files to ignore
```

o

## Types of Repositories

### Local Repository

- Stored on your machine
- Contains complete project history
- Works offline
- Created with [[git-init]] or [[git-clone]]

### Remote Repository

- Stored on external servers (GitHub, GitLab, etc.)
- Shared among team members
- Backup and collaboration point
- Connected via [[git-remote]]

### Bare Repository

- Contains only Git data (no working directory)
- Used for servers and sharing
- Created with `git init --bare`
- Cannot checkout files directly

## Repository States

### Clean Repository

- No uncommitted changes
- [[WorkingDirectory]] matches latest commit
- Safe to switch branches

### Dirty Repository

- Has uncommitted changes
- Files modified since last commit
- May need [[git-stash]] before switching branches

## Creating Repositories

### Initialize New Repository

```bash
# Create new repository
git init

# Create with specific branch name
git init --initial-branch=main
```

### Clone Existing Repository

```bash
# Clone from remote
git clone https://github.com/user/repo.git

# Clone to specific directory
git clone https://github.com/user/repo.git my-project
```

## Repository Information

### Check Repository Status

```bash
# See repository state
git status

# Check remote connections
git remote -v

# View repository configuration
git config --list --local
```

### Repository Statistics

```bash
# Count objects and size
git count-objects -v

# Repository size breakdown
du -sh .git/

# All branches and tags
git branch -a && git tag
```

## Best Practices

### Repository Organization

- Keep repository focused on single project
- Use clear directory structure
- Include comprehensive README
- Set up appropriate [[GitIgnorePatterns]]

### Repository Maintenance

- Regular [[git-gc]] for optimization
- Monitor repository size growth
- Clean up old branches periodically
- Use [[git-fsck]] to check integrity

## Common Repository Tasks

### Repository Setup

1. [[GitInstallation]] - Install Git
2. [[GitConfiguration]] - Set identity
3. [[RepositoryInitialization]] - Create repo
4. [[FirstCommit]] - Initial snapshot

### Daily Operations

1. [[git-status]] - Check changes
2. [[git-add]] - Stage changes
3. [[git-commit]] - Save snapshots
4. [[git-push]] - Share changes

## Repository Patterns

### Single Repository

- One project per repository
- Simplest approach
- Easy to manage permissions

### Monorepo

- Multiple projects in one repository
- Shared dependencies and tools
- Complex but coordinated development

### Submodules

- Repositories within repositories
- Independent project lifecycles
- See [[git-submodule]]

## Repository Security

### Access Control

- Use SSH keys for authentication
- Set up proper permissions
- Consider private repositories

### Sensitive Data

- Never commit passwords or keys
- Use [[GitIgnorePatterns]] properly
- Consider [[git-filter-branch]] for cleanup

## Troubleshooting

### Common Repository Issues

- [[CorruptedRepository]] - Recovery techniques
- [[PermissionDenied]] - Access problems
- [[LargeFileIssues]] - Size management
- [[SlowGitOperations]] - Performance tuning

### Repository Recovery

- [[git-fsck]] - Check integrity
- [[git-reflog]] - Find lost commits
- Backup and restore strategies

## Related Notes

- [[WorkingDirectory]] - Your project files
- [[StagingArea]] - Preparing commits
- [[GitHistory]] - Stored changes
- [[Remote]] - External repositories
- [[Branch]] - Parallel development

