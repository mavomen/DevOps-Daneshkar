---
id: git-config
aliases: []
tags: []
---

# git config

Read and write Git configuration values (user identity, editor, aliases, behavior).

## Syntax

```bash
git config [<options>] --list
git config [<options>] <name>
git config [<options>] <name> <value>
git config [<options>] --unset <name>
git config [<options>] --edit
```

## Description

`git config` manages configuration at three main scopes (highest priority first):

| Scope  | Flag       | Applies to        | Typical file   |
| ------ | ---------- | ----------------- | -------------- |
| Local  | `--local`  | current repo only | `.git/config`  |
| Global | `--global` | current user      | `~/.gitconfig` |
| System | `--system` | all users         | varies by OS   |

> If you don’t specify a scope, Git chooses a default depending on context, but being explicit is safer in scripts.

## Common Usage

### Show effective config (with sources)

```bash
git config --list --show-origin
```

### Get a value

```bash
git config user.name
git config --global core.editor
```

### Set a value

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global core.editor "code --wait"
```

### Unset a value

```bash
git config --global --unset core.editor
```

### Edit config files directly (in your editor)

```bash
git config --global --edit
git config --local --edit
```

## Helpful Options

### Work with a specific scope

```bash
git config --local user.email
git config --global pull.rebase true
git config --system --list
```

### Show where a value came from

```bash
git config --show-origin user.email
```

### Add multiple values to the same key

Example: multiple `url.<base>.insteadOf` values.

```bash
git config --global --add url."git@github.com:".insteadOf https://github.com/
```

### Remove all values for a multi-valued key

```bash
git config --global --unset-all url."git@github.com:".insteadOf
```

## Practical Examples

### Set default branch name

```bash
git config --global init.defaultBranch main
```

### Configure line endings

```bash
# Linux/macOS typical
git config --global core.autocrlf input

# Windows typical
git config --global core.autocrlf true
```

See: [[GitAttributes]]

### Create aliases

```bash
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --decorate --all"
```

See: [[GitAliases]]

## Troubleshooting

### “error: key does not contain a section”

Keys must be in `section.key` form, e.g.:

- `user.name`
- `core.editor`
- `pull.rebase`

### Confusing behavior / unexpected value

Check all scopes + sources:

```bash
git config --list --show-origin
```

## Related Notes

- [[GitConfiguration]]
- [[GitAliases]]
- [[EditorIntegration]]
- [[SshKeysSetup]]
- [[git-credential]]
