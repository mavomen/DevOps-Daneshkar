---
id: git-init
aliases: []
tags: []
---

# git init

Initialize a new Git repository in the current directory or create a new repository with a specific directory structure.

## Syntax

```bash
git init [<directory>]
git init [options]
```

## Description

The `git init` command creates a new Git repository by setting up the initial directory structure and files needed for version control. It creates a `.git` subdirectory that contains all the necessary Git metadata and object database.

## Basic Usage

### Initialize Current Directory

```bash
# Initialize Git repository in current directory
git init
```

### Initialize New Directory

```bash
# Create and initialize new directory
git init my-project

# Equivalent to:
mkdir my-project
cd my-project
git init
```

### Initialize with Specific Branch Name

```bash
# Initialize with 'main' as default branch
git init --initial-branch=main
git init -b main

# Initialize with custom default branch
git init --initial-branch=develop
```

## What git init Creates

### Directory Structure

```
project/
└── .git/
    ├── branches/
    ├── config
    ├── description
    ├── HEAD
    ├── hooks/
    │   ├── pre-commit.sample
    │   ├── pre-push.sample
    │   └── ...
    ├── info/
    │   └── exclude
    ├── objects/
    │   ├── info/
    │   └── pack/
    └── refs/
        ├── heads/
        └── tags/
```

### Key Files Created

- **HEAD**: Points to current branch
- **config**: Repository-specific configuration
- **description**: Repository description for GitWeb
- **hooks/**: Sample hook scripts
- **objects/**: Git object database
- **refs/**: Branch and tag references

## Options

### Branch Configuration

```bash
# Set default branch name
git init --initial-branch=<name>
git init -b <name>

# Use system default branch name
git init  # Uses init.defaultBranch config
```

### Repository Type

```bash
# Create bare repository (no working directory)
git init --bare

# Create shared repository
git init --shared[=<permissions>]
```

### Template Directory

```bash
# Use custom template
git init --template=<template-directory>

# Use system default template
git init  # Uses init.templateDir config
```

### Quiet Mode

```bash
# Suppress output
git init --quiet
git init -q
```

## Advanced Usage

### Bare Repository

```bash
# Create bare repository for server/sharing
git init --bare project.git

# Bare repositories:
# - No working directory
# - Only .git contents
# - Can be pushed to by multiple users
# - Common for central repositories
```

### Shared Repository

```bash
# Create shared repository with group permissions
git init --shared=group

# Permission options:
# false/umask: Use default umask
# group/true: Make repository group-writable
# all/world/everybody: Make repository readable by all
# 0xxx: Custom octal permissions
```

### Repository Templates

```bash
# Create repository with custom template
git init --template=/path/to/template

# Template directory can contain:
# - hooks/: Custom hook scripts
# - info/exclude: Default ignore patterns
# - description: Repository description
# - config: Default configuration
```

## After Initialization

### First Steps

```bash
# 1. Initialize repository
git init

# 2. Configure user identity (if not set globally)
git config user.name "Your Name"
git config user.email "your.email@example.com"

# 3. Create initial files
echo "# My Project" > README.md
echo "node_modules/" > .gitignore

# 4. Stage and commit initial files
git add .
git commit -m "Initial commit"
```

### Connect to Remote

```bash
# Add remote origin
git remote add origin https://github.com/user/repo.git

# Push initial commit
git push -u origin main
```

## Common Workflows

### New Local Project

```bash
# Start new project
mkdir my-app
cd my-app
git init

# Set up project structure
mkdir src docs
echo "# My App" > README.md
echo "dist/" > .gitignore

# Initial commit
git add .
git commit -m "Initial project setup"
```

### Convert Existing Project

```bash
# Navigate to existing project
cd existing-project

# Initialize Git
git init

# Add existing files
git add .
git commit -m "Initial import of existing project"

# Connect to remote (optional)
git remote add origin <repository-url>
git push -u origin main
```

### Create Repository for Collaboration

```bash
# Create bare repository on server
ssh server.com
mkdir /path/to/repo.git
cd /path/to/repo.git
git init --bare --shared=group

# Clone on local machine
git clone server.com:/path/to/repo.git
cd repo
# Start working...
```

## Configuration After Init

### Repository-Specific Config

```bash
# Set local configuration
git config user.name "Project Specific Name"
git config user.email "project@company.com"

# Set default branch
git config init.defaultBranch main

# Configure line endings
git config core.autocrlf input  # Unix-like systems
git config core.autocrlf true   # Windows

# Set editor
git config core.editor "code --wait"
```

### Set Up Hooks

```bash
# Enable pre-commit hook
cd .git/hooks
cp pre-commit.sample pre-commit
chmod +x pre-commit

# Edit hook content
vim pre-commit
```

## Common Use Cases

### Personal Project

```bash
git init
git config user.name "John Doe"
git config user.email "john@personal.com"
echo "# Personal Project" > README.md
git add README.md
git commit -m "Initial commit"
```

### Team Project

```bash
git init --initial-branch=develop
git config user.name "John Doe"
git config user.email "john@company.com"

# Set up team structure
mkdir docs src tests
echo "# Team Project" > README.md
echo "node_modules/\n*.log\n.env" > .gitignore
git add .
git commit -m "Initial team project setup"

# Connect to team repository
git remote add origin https://github.com/company/project.git
git push -u origin develop
```

### Server Repository

```bash
# On server
sudo mkdir /git/project.git
sudo chown git:git /git/project.git
cd /git/project.git
sudo -u git git init --bare --shared=group

# Team members clone:
git clone git@server:/git/project.git
```

## Troubleshooting

### Already a Git Repository

```bash
# Error: "already exists"
# Check if .git already exists
ls -la

# If reinitialization needed:
rm -rf .git  # BE CAREFUL - destroys Git history
git init
```

### Permission Issues

```bash
# Fix ownership issues
sudo chown -R user:group .git

# Fix shared repository permissions
git init --shared=group
chmod -R g+ws .git
```

### Wrong Initial Branch

```bash
# Change default branch after init
git branch -m master main
git symbolic-ref HEAD refs/heads/main
```

## Best Practices

### Before Initializing

- Choose appropriate directory name
- Plan repository structure
- Consider if bare repository is needed
- Set up global Git configuration first

### After Initializing

- Configure user identity if needed
- Create meaningful .gitignore file
- Set up project structure
- Make initial commit with clear message
- Connect to remote repository if needed

### Team Repositories

- Use consistent branch naming
- Set up shared repository permissions
- Document repository conventions
- Configure branch protection rules
- Set up continuous integration

## Related Commands

- [[git-clone]] - Copy existing repository
- [[git-config]] - Configure repository
- [[git-remote]] - Manage remote repositories
- [[git-status]] - Check repository state

## Examples

```bash
# Simple project initialization
git init my-website
cd my-website
echo "<h1>My Website</h1>" > index.html
git add index.html
git commit -m "Initial website setup"

# Team project with structure
git init --initial-branch=develop team-project
cd team-project
mkdir src tests docs
echo "# Team Project" > README.md
echo "*.log\nnode_modules/\n.env" > .gitignore
git add .
git commit -m "Initial project structure"

# Server repository setup
git init --bare --shared=group /path/to/shared/repo.git
```

---

tags: #git #command #setup #initialization #repository

````

## Commands/Setup/git-config.md

```markdown
# git config

Configure Git settings at different levels (system, global, local) to customize behavior, identity, and preferences.

## Syntax

```bash
git config [<level>] <key> [<value>]
git config [<level>] [options]
````

## Configuration Levels

Git configuration operates at three levels with different priorities:

| Level      | Scope              | File Location    | Priority |
| ---------- | ------------------ | ---------------- | -------- |
| `--system` | All users          | `/etc/gitconfig` | Lowest   |
| `--global` | Current user       | `~/.gitconfig`   | Medium   |
| `--local`  | Current repository | `.git/config`    | Highest  |

## Basic Usage

### Set Configuration Values

```bash
# Set global configuration
git config --global user.name "John Doe"
git config --global user.email "john@example.com"

# Set local (repository-specific) configuration
git config --local user.name "Work Name"
git config --local user.email "work@company.com"

# Set system-wide configuration (requires admin)
sudo git config --system init.defaultBranch main
```

### Get Configuration Values

```bash
# Get specific value
git config user.name
git config user.email

# Get with level specification
git config --global user.email
git config --local core.editor

# Get all configuration
git config --list

# Get configuration with origin
git config --list --show-origin
```

## Essential Configuration

### User Identity

```bash
# Required for commits
git config --global user.name "Your Full Name"
git config --global user.email "your.email@example.com"

# Verify identity
git config user.name
git config user.email
```

### Default Editor

```bash
# Set preferred editor
git config --global core.editor "code --wait"    # VS Code
git config --global core.editor "vim"            # Vim
git config --global core.editor "nano"           # Nano
git config --global core.editor "subl -w"        # Sublime Text

# For Windows
git config --global core.editor "notepad"        # Notepad
git config --global core.editor "'C:\Program Files\Notepad++\notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
```

### Default Branch

```bash
# Set default branch name for new repositories
git config --global init.defaultBranch main

# Alternative names
git config --global init.defaultBranch master
git config --global init.defaultBranch develop
```

### Line Ending Configuration

```bash
# For Unix/Linux/macOS (recommended)
git config --global core.autocrlf input

# For Windows
git config --global core.autocrlf true

# Disable line ending conversion
git config --global core.autocrlf false
```

## Advanced Configuration

### Credential Management

```bash
# Cache credentials for 15 minutes (default)
git config --global credential.helper cache

# Cache credentials for 1 hour
git config --global credential.helper "cache --timeout=3600"

# Store credentials permanently (less secure)
git config --global credential.helper store

# Use system credential manager
git config --global credential.helper manager-core  # Cross-platform
git config --global credential.helper osxkeychain   # macOS
git config --global credential.helper wincred       # Windows
```

### Merge and Diff Tools

```bash
# Set merge tool
git config --global merge.tool vimdiff
git config --global merge.tool kdiff3
git config --global merge.tool meld

# Set diff tool
git config --global diff.tool vimdiff

# Configure VS Code as merge/diff tool
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'
git config --global diff.tool vscode
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'
```

### Push Configuration

```bash
# Set default push behavior
git config --global push.default simple    # Push current branch to same name
git config --global push.default current   # Push current branch to upstream
git config --global push.default upstream  # Push current branch to upstream
git config --global push.default nothing   # Require explicit branch specification

# Automatically set up tracking for new branches
git config --global push.autoSetupRemote true
```

### Pull Configuration

```bash
# Set default pull behavior
git config --global pull.rebase false   # Merge (default)
git config --global pull.rebase true    # Rebase
git config --global pull.ff only        # Only fast-forward
```

## Aliases Configuration

### Basic Aliases

```bash
# Common shortcuts
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.pl pull
git config --global alias.ps push
```

### Advanced Aliases

```bash
# Enhanced log displays
git config --global alias.lg "log --oneline --graph --decorate --all"
git config --global alias.hist "log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short"

# Useful shortcuts
git config --global alias.unstage "restore --staged"
git config --global alias.last "log -1 HEAD"
git config --global alias.visual "!gitk"
```

## Configuration Management

### Viewing Configuration

```bash
# List all configuration
git config --list

# List with file origins
git config --list --show-origin

# List specific level
git config --list --global
git config --list --local
git config --list --system

# Show specific section
git config --get-regexp user
git config --get-regexp alias
```

### Editing Configuration

```bash
# Edit global configuration file
git config --global --edit

# Edit local configuration file
git config --local --edit

# Edit system configuration file
sudo git config --system --edit
```

### Removing Configuration

```bash
# Remove specific setting
git config --global --unset user.name
git config --local --unset core.editor

# Remove entire section
git config --global --remove-section alias

# Remove all entries matching pattern
git config --global --unset-all user.email
```

## Conditional Configuration

### Include Other Config Files

```bash
# Include additional config file
git config --global include.path ~/.gitconfig-work

# Conditional includes based on directory
git config --global includeIf."gitdir:~/work/".path ~/.gitconfig-work
git config --global includeIf."gitdir:~/personal/".path ~/.gitconfig-personal
```

### Example Conditional Setup

```bash
# ~/.gitconfig
[includeIf "gitdir:~/work/"]
    path = ~/.gitconfig-work
[includeIf "gitdir:~/personal/"]
    path = ~/.gitconfig-personal

# ~/.gitconfig-work
[user]
    name = John Doe
    email = john@company.com
[core]
    sshCommand = ssh -i ~/.ssh/work_key

# ~/.gitconfig-personal
[user]
    name = John Doe
    email = john@personal.com
[core]
    sshCommand = ssh -i ~/.ssh/personal_key
```

## Security Configuration

### Signing Configuration

```bash
# Set up commit signing
git config --global user.signingkey <GPG-KEY-ID>
git config --global commit.gpgsign true
git config --global tag.gpgsign true

# Configure GPG program
git config --global gpg.program gpg2
```

### SSH Configuration

```bash
# Set custom SSH command
git config --global core.sshCommand "ssh -i ~/.ssh/custom_key"

# Per-repository SSH key
git config core.sshCommand "ssh -i ~/.ssh/repo_specific_key"
```

## Performance Configuration

### Large Repository Settings

```bash
# Enable file system monitor for large repos
git config --global core.fsmonitor true

# Enable parallel index preload
git config --global core.preloadindex true

# Set pack size limits
git config --global pack.packSizeLimit 2g
```

### Network Settings

```bash
# Set HTTP timeout
git config --global http.timeout 300

# Enable HTTP connection reuse
git config --global http.postBuffer 524288000

# Set proxy
git config --global http.proxy http://proxy.company.com:8080
```

## Common Configuration Patterns

### Developer Setup

```bash
#!/bin/bash
# Basic Git setup script

# Identity
git config --global user.name "Developer Name"
git config --global user.email "dev@example.com"

# Editor and tools
git config --global core.editor "code --wait"
git config --global merge.tool vscode
git config --global diff.tool vscode

# Behavior
git config --global init.defaultBranch main
git config --global pull.rebase true
git config --global push.autoSetupRemote true

# Line endings (adjust for OS)
git config --global core.autocrlf input  # Unix/Mac
# git config --global core.autocrlf true   # Windows

# Aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --all"
```

### Team Configuration

```bash
# Consistent team settings
git config --global core.autocrlf input
git config --global init.defaultBranch main
git config --global pull.rebase true
git config --global push.default current

# Enforce signing
git config --global commit.gpgsign true
git config --global tag.gpgsign true

# Set merge strategy
git config --global merge.ours.driver true
```

## Troubleshooting Configuration

### Check Current Settings

```bash
# Debug configuration issues
git config --list --show-origin | grep user
git config --get user.name
git config --get user.email

# Check which config file is being used
git config --show-origin user.name
```

### Fix Common Issues

```bash
# Reset corrupted config
mv ~/.gitconfig ~/.gitconfig.backup
git config --global --list  # Will be empty

# Fix encoding issues
git config --global core.quotepath false
git config --global core.unicode true

# Fix line ending issues
git config --global core.autocrlf input
git add --renormalize .
```

### Verify Configuration

```bash
# Test configuration
git config --get user.name
git config --get user.email
git config --list | grep -E "user|core|alias"

# Check effective configuration for repository
cd /path/to/repo
git config --list --show-origin
```

## Best Practices

### Initial Setup

1. Set user identity first
2. Configure editor and tools
3. Set up aliases for efficiency
4. Configure line endings for your OS
5. Set up credential caching

### Team Coordination

1. Document team configuration standards
2. Use consistent settings across team
3. Set up conditional configuration for different projects
4. Share useful aliases
5. Configure security settings appropriately

### Maintenance

1. Review configuration periodically
2. Clean up unused settings
3. Back up important configuration
4. Test configuration changes
5. Document custom settings

## Related Commands

- [[git-init]] - Uses configuration for new repositories
- [[git-clone]] - Inherits configuration settings
- [[GitAliases]] - Custom command shortcuts
- [[git-credential]] - Credential management

## Quick Reference

| Command                                  | Purpose                 |
| ---------------------------------------- | ----------------------- |
| `git config --global user.name "Name"`   | Set global username     |
| `git config --global user.email "email"` | Set global email        |
| `git config --list`                      | Show all configuration  |
| `git config --edit`                      | Edit configuration file |
| `git config --unset <key>`               | Remove configuration    |
