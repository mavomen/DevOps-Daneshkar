---
id: GitConfiguration
aliases: []
tags: []
---

# Git Configuration

Configure Git identity and behavior (editor, defaults, line endings, credential helpers, etc.).

## Suggested Aliases (optional)

- `Git Configuration`

## Config Scopes (Priority)

| Scope  | Flag       | Applies to        | Typical file   |
| ------ | ---------- | ----------------- | -------------- |
| Local  | `--local`  | current repo only | `.git/config`  |
| Global | `--global` | current user      | `~/.gitconfig` |
| System | `--system` | all users         | varies by OS   |

Check effective configuration:

```bash
git config --list --show-origin
```

## Identity (Required)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Verify:

```bash
git config user.name
git config user.email
```

## Editor

```bash
git config --global core.editor "nvim"
# or
git config --global core.editor "code --wait"
```

## Default Branch Name

```bash
git config --global init.defaultBranch main
```

## Line Endings (Autocrlf)

### Recommended defaults

- Linux/macOS:

```bash
git config --global core.autocrlf input
```

- Windows:

```bash
git config --global core.autocrlf true
```

> If your team enforces consistent line endings, also see [[GitAttributes]].

## Credential Helper (HTTPS)

Examples:

```bash
git config --global credential.helper cache
git config --global credential.helper manager-core
```

## Pull Behavior

```bash
# merge-style pull (default)
git config --global pull.rebase false

# rebase-style pull
git config --global pull.rebase true

# only fast-forward on pull
git config --global pull.ff only
```

## Useful “audit” commands

```bash
git config --list
git config --list --show-origin
git config --global --edit
git config --local --edit
```

## Related Notes

- [[GitInstallation]]
- [[GitAliases]]
- [[SshKeysSetup]]
- [[GitIgnorePatterns]]
- [[GitAttributes]]
- [[git-config]]
