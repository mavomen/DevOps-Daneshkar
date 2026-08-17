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

## Related Notes

- [[git-clone]] - Copy existing repository
- [[git-config]] - Configure repository
- [[git-remote]] - Manage remote repositories
- [[git-status]] - Check repository state
