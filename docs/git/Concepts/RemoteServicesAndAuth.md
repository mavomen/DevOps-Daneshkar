---
id: RemoteServicesAndAuth
aliases: []
tags: []
---

# Remote Services & Auth

## Authentication

### HTTPS Authentication

```bash
# Store credentials temporarily
git config credential.helper cache

# Store credentials permanently (less secure)
git config credential.helper store

# Use system credential manager
git config credential.helper manager-core
```

### SSH Authentication

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your-email@example.com"

# Add key to SSH agent
ssh-add ~/.ssh/id_ed25519

# Test SSH connection
ssh -T git@github.com

# Clone with SSH
git clone git@github.com:user/repo.git
```

## Remote Hosting Services

### GitHub

- Most popular Git hosting
- Pull requests and issues
- GitHub Actions for CI/CD
- Large open source community

### GitLab

- Self-hosted or cloud
- Built-in CI/CD
- Issue tracking and wiki
- Strong DevOps integration

### Bitbucket

- Atlassian ecosystem
- Integration with Jira
- Bamboo CI/CD
- Enterprise features

### Self-hosted

- Complete control
- Custom setup and security
- GitLab CE, Gitea, Gogs
- Integration with existing infrastructure

## Multiple Remotes

### Working with Multiple Remotes

```bash
# Add upstream for fork workflow
git remote add upstream https://github.com/original/repo.git

# Fetch from upstream
git fetch upstream

# Merge upstream changes
git merge upstream/main

# Push to your fork
git push origin main

# Different URLs for fetch/push
git remote set-url --push origin git@github.com:user/repo.git
```

### Remote Management Strategy

```bash
# Check all remotes
git remote -v

# Sync with upstream regularly
git fetch upstream
git merge upstream/main
git push origin main

# Keep fork updated
git pull upstream main
git push origin main
```

## Troubleshooting Remotes

### Common Remote Issues

```bash
# Remote URL changed
git remote set-url origin new-url

# Permission denied
# Check SSH keys or credentials

# Branch doesn't exist on remote
git push -u origin local-branch

# Remote ahead of local
git pull origin main
git push origin main
```

### Connection Problems

```bash
# Test remote connection
git ls-remote origin

# Check network connectivity
ping github.com

# Verify SSH setup
ssh -T git@github.com

# Check HTTPS credentials
git credential fill
```

## Remote Best Practices

### Repository Setup

- Use SSH for better security
- Set up credential caching
- Use meaningful remote names
- Document remote conventions

### Daily Workflow

- Fetch regularly to stay updated
- Pull before starting work
- Push finished work promptly
- Use pull requests for collaboration

### Team Coordination

- Agree on branching strategy
- Document remote setup process
- Use consistent naming conventions
- Protect important branches

## Advanced Remote Features

### Partial Clone

```bash
# Clone without downloading all objects
git clone --filter=blob:none https://github.com/user/repo.git

# Clone only recent history
git clone --depth=10 https://github.com/user/repo.git
```

### Sparse Checkout

```bash
# Clone and checkout only specific directories
git clone --filter=blob:none --sparse https://github.com/user/repo.git
cd repo
git sparse-checkout init --cone
git sparse-checkout set src docs
```

## Related Notes

- [[Remote]] — Core concepts
- [[RemoteServicesAndAuth]] — This note
