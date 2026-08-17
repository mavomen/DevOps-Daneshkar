---
id: git-config
aliases: []
tags: []
---

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

## Related Notes

- [[git-init]] - Uses configuration for new repositories
- [[git-clone]] - Inherits configuration settings
- [[GitAliases]] - Custom command shortcuts
- [[git-credential]] - Credential management

