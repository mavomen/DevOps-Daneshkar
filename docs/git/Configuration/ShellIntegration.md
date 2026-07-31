---
id: ShellIntegration
aliases: []
tags: []
---

# Shell Integration

Improve your terminal Git workflow with completion, prompt info, and useful config.

## Suggested Aliases (optional)

- `Shell Integration`

## Git Completion

### Bash (common)

Install your distro’s completion package (varies), then ensure completion is enabled.

Quick check (bash):

```bash
complete -p git
```

### Zsh

If you use a framework (like oh-my-zsh), Git completion is usually included.

## Useful Git Config for Terminal UX

### Better paging / colors

```bash
git config --global color.ui auto
git config --global core.pager "less -FRSX"
```

### Helpful status output

```bash
git config --global status.branch true
git config --global status.short true
```

## Prompt Integration (Conceptual)

Most prompts show:

- current branch
- dirty state
- ahead/behind of upstream

That relies on upstream tracking (see [[UpstreamAndOrigin]]).

## Quality-of-life aliases (Git-level)

See: [[GitAliases]]

## Related Notes

- [[GitAliases]]
- [[GitConfiguration]]
- [[UpstreamAndOrigin]]
