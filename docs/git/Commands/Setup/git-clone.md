---
id: git-clone
aliases: []
tags: []
---

# git clone

Create a local copy of a remote Git repository, including all files, history, and branches.

## Syntax

```bash
git clone [<options>] <repository> [<directory>]
```

## Description

The `git clone` command creates a complete copy of a remote [[Repository]], including all commit history, branches, and tags. It automatically sets up a connection to the original repository as a [[Remote]] called "origin" and checks out the default branch.

## Basic Usage

### Clone Repository

```bash
# Clone to directory with same name as repository
git clone https://github.com/user/repo.git

# Clone to specific directory
git clone https://github.com/user/repo.git my-project

# Clone with different remote name
git clone -o upstream https://github.com/user/repo.git
```

### Clone Protocols

```bash
# HTTPS (most common)
git clone https://github.com/user/repo.git

# SSH (requires SSH key setup)
git clone git@github.com:user/repo.git

# Local file system
git clone /path/to/local/repo.git
git clone file:///path/to/local/repo.git
```

## Clone Options

### Branch Selection

```bash
# Clone specific branch only
git clone -b feature-branch https://github.com/user/repo.git

# Clone specific branch with custom directory name
git clone -b develop https://github.com/user/repo.git my-project
```

### Depth Control

```bash
# Shallow clone (only recent history)
git clone --depth 1 https://github.com/user/repo.git

# Clone with specific depth
git clone --depth 10 https://github.com/user/repo.git

# Clone since specific date
git clone --shallow-since="2024-01-01" https://github.com/user/repo.git
```

### Partial Clone

```bash
# Clone without downloading all objects immediately
git clone --filter=blob:none https://github.com/user/repo.git

# Clone only specific directories (requires Git 2.25+)
git clone --filter=blob:none --sparse https://github.com/user/repo.git
cd repo
git sparse-checkout init --cone
git sparse-checkout set src docs
```

### Recursive Cloning

```bash
# Clone with submodules
git clone --recurse-submodules https://github.com/user/repo.git

# Clone and initialize submodules
git clone --recursive https://github.com/user/repo.git
```

## Advanced Options

### Network and Performance

```bash
# Clone with progress indication
git clone --progress https://github.com/user/repo.git

# Clone quietly (suppress output)
git clone --quiet https://github.com/user/repo.git

# Clone with custom configuration
git clone -c core.autocrlf=false https://github.com/user/repo.git

# Clone with specific remote name
git clone --origin upstream https://github.com/user/repo.git
```

### Bare Repository

```bash
# Clone as bare repository (no working directory)
git clone --bare https://github.com/user/repo.git

# Useful for:
# - Server repositories
# - Backup repositories
# - Mirror repositories
```

### Template Usage

```bash
# Clone with custom template
git clone --template=/path/to/template https://github.com/user/repo.git
```

## What git clone Creates

### Directory Structure

```
my-project/
├── .git/                 # Git database and configuration
│   ├── config           # Repository configuration
│   ├── objects/         # Object database
│   ├── refs/            # Branch and tag references
│   └── ...
├── src/                 # Project files
├── docs/                # Documentation
├── README.md            # Project description
└── .gitignore          # Ignore patterns
```

### Automatic Setup

```bash
# After cloning, Git automatically sets up:
# 1. Remote "origin" pointing to source repository
git remote -v
# origin  https://github.com/user/repo.git (fetch)
# origin  https://github.com/user/repo.git (push)

# 2. Local branch tracking remote default branch
git branch -vv
# * main 1a2b3c4 [origin/main] Latest commit message

# 3. All remote references
git branch -r
# origin/main
# origin/feature-1
# origin/feature-2
```

## Common Workflows

### Basic Project Setup

```bash
# Clone repository
git clone https://github.com/user/awesome-project.git

# Navigate to project
cd awesome-project

# Check status and branches
git status
git branch -a

# Start working
# ... make changes ...
git add .
git commit -m "Initial local changes"
git push origin main
```

### Fork and Clone Workflow

```bash
# 1. Fork repository on GitHub/GitLab
# 2. Clone your fork
git clone https://github.com/yourusername/forked-repo.git

# 3. Add upstream remote
cd forked-repo
git remote add upstream https://github.com/originaluser/repo.git

# 4. Verify remotes
git remote -v
# origin    https://github.com/yourusername/forked-repo.git (fetch)
# origin    https://github.com/yourusername/forked-repo.git (push)
# upstream  https://github.com/originaluser/repo.git (fetch)
# upstream  https://github.com/originaluser/repo.git (push)

# 5. Keep fork updated
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### Multiple Remote Setup

```bash
# Clone original repository
git clone https://github.com/company/project.git

# Add your fork as additional remote
cd project
git remote add myfork https://github.com/yourusername/project.git

# Add team member's fork
git remote add teammate https://github.com/teammate/project.git

# View all remotes
git remote -v
```

## Cloning Strategies

### Quick Start Development

```bash
# Shallow clone for quick start
git clone --depth 1 https://github.com/user/large-repo.git

# Later, if you need full history
cd large-repo
git fetch --unshallow
```

### Large Repository Handling

```bash
# Partial clone for large repositories
git clone --filter=blob:limit=1m https://github.com/user/huge-repo.git

# Clone specific branch only
git clone -b main --single-branch https://github.com/user/repo.git

# Combine shallow and single branch
git clone --depth 1 -b main --single-branch https://github.com/user/repo.git
```

### Submodule Projects

```bash
# Clone project with submodules
git clone --recurse-submodules https://github.com/user/project-with-submodules.git

# If you forgot --recurse-submodules
git clone https://github.com/user/project-with-submodules.git
cd project-with-submodules
git submodule init
git submodule update

# Or in one command
git submodule update --init --recursive
```

## Authentication

### HTTPS with Credentials

```bash
# Clone with username in URL
git clone https://username@github.com/user/private-repo.git

# Git will prompt for password or token
# Better: Set up credential helper
git config --global credential.helper cache
git clone https://github.com/user/private-repo.git
```

### SSH Authentication

```bash
# Set up SSH key (one time)
ssh-keygen -t ed25519 -C "your-email@example.com"
ssh-add ~/.ssh/id_ed25519
# Add public key to GitHub/GitLab

# Clone with SSH
git clone git@github.com:user/repo.git

# Test SSH connection
ssh -T git@github.com
```

### Personal Access Tokens

```bash
# Create token on GitHub/GitLab
# Clone using token as password
git clone https://github.com/user/private-repo.git
# Username: your-username
# Password: your-personal-access-token

# Or embed token in URL (less secure)
git clone https://your-username:your-token@github.com/user/private-repo.git
```

## Troubleshooting

### Common Clone Issues

```bash
# Permission denied (SSH)
# Solution: Check SSH key setup
ssh -T git@github.com
ssh-add -l

# Repository not found (HTTPS)
# Solution: Check URL and permissions
curl -I https://github.com/user/repo.git

# SSL certificate problems
# Solution: Update certificates or disable SSL verification
git config --global http.sslVerify false  # Not recommended for production

# Large repository timeout
# Solution: Use shallow clone or increase timeout
git config --global http.timeout 300
git clone --depth 1 https://github.com/user/large-repo.git
```

### Network Issues

```bash
# Clone behind proxy
git config --global http.proxy http://proxy.company.com:8080
git clone https://github.com/user/repo.git

# Clone with custom SSL bundle
git config --global http.sslCAInfo /path/to/certificates.pem
git clone https://internal-git.company.com/repo.git

# Clone with increased buffer
git config --global http.postBuffer 524288000
git clone https://github.com/user/large-repo.git
```

### Incomplete Clones

```bash
# Resume interrupted clone
cd partial-repo
git fetch origin
git reset --hard origin/main

# Fix corrupted clone
rm -rf corrupted-repo
git clone --depth 1 https://github.com/user/repo.git
cd repo
git fetch --unshallow
```

## Post-Clone Configuration

### Repository Setup

```bash
# Clone repository
git clone https://github.com/user/project.git
cd project

# Set up user configuration
git config user.name "Your Name"
git config user.email "your.email@example.com"

# Set up upstream remote (for forks)
git remote add upstream https://github.com/originaluser/project.git

# Set up additional remotes
git remote add staging https://github.com/company/project-staging.git
```

### Branch Setup

```bash
# Check out specific branch
git checkout -b develop origin/develop

# Set up tracking for all remote branches
git branch -r | grep -v '\->' | while read remote; do
    git branch --track "${remote#origin/}" "$remote"
done
```

## Best Practices

### Before Cloning

- Verify repository URL and permissions
- Choose appropriate clone method (HTTPS vs SSH)
- Consider if shallow clone is sufficient
- Check repository size for large repositories

### After Cloning

- Configure user identity if different from global
- Set up additional remotes if needed
- Review repository structure and documentation
- Install dependencies and verify setup

### Security

- Use SSH keys for private repositories
- Don't embed credentials in URLs
- Use credential helpers for HTTPS
- Verify repository authenticity

## Performance Tips

### Large Repositories

```bash
# Use partial clone for huge repositories
git clone --filter=blob:limit=1m https://github.com/user/huge-repo.git

# Use shallow clone for CI/CD
git clone --depth 1 https://github.com/user/repo.git

# Clone specific branch only
git clone -b main --single-branch https://github.com/user/repo.git
```

### Network Optimization

```bash
# Increase buffer for large repositories
git config --global http.postBuffer 1048576000

# Enable parallel fetching
git config --global fetch.parallel 8

# Use compression
git config --global core.compression 9
```

## Related Commands

- [[git-remote]] - Manage remote repositories
- [[git-fetch]] - Download from remotes
- [[git-pull]] - Fetch and merge from remotes
- [[RepositoryInitialization]] - Creating new repositories
- [[git-submodule]] - Managing submodules

## Examples

```bash
# Basic clone
git clone https://github.com/torvalds/linux.git

# Clone with custom directory name
git clone https://github.com/facebook/react.git my-react-project

# Shallow clone for quick exploration
git clone --depth 1 https://github.com/microsoft/vscode.git

# Clone specific branch
git clone -b develop https://github.com/user/project.git

# Clone with submodules
git clone --recurse-submodules https://github.com/user/project-with-submodules.git
```
