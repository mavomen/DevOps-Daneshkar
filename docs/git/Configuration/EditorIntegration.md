---
id: EditorIntegration
aliases: []
tags: []
---

# Editor Integration

Configure your editor as Git’s commit-message editor and (optionally) diff/merge tool.

## Suggested Aliases (optional)

- `Editor Integration`

## Configure Commit Editor

### VS Code

```bash
git config --global core.editor "code --wait"
```

### Neovim / Vim

```bash
git config --global core.editor "nvim"
# or
git config --global core.editor "vim"
```

### Nano

```bash
git config --global core.editor "nano"
```

## One-off Editor Override

Environment variables override config:

```bash
GIT_EDITOR=nvim git commit
```

## Diff Tool Integration (Optional)

### VS Code difftool

```bash
git config --global diff.tool vscode
git config --global difftool.vscode.cmd "code --wait --diff \$LOCAL \$REMOTE"
git config --global difftool.prompt false
```

Use:

```bash
git difftool
git difftool --staged
```

## Merge Tool Integration (Optional)

### VS Code mergetool

```bash
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd "code --wait \$MERGED"
git config --global mergetool.prompt false
```

Use:

```bash
git mergetool
```

## Related Notes

- [[GitConfiguration]]
- [[git-commit]]
- [[git-diff]]
- [[git-merge]]
