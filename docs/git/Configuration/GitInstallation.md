---
id: GitInstallation
aliases: []
tags: []
---

# Git Installation

Install Git on your system and verify it’s working.

## Suggested Aliases (optional)

If your vault already links to names with spaces, add aliases in Obsidian properties:

- `Git Installation`

## Verify Installation

```bash
git --version
git version
```

## Linux

### Arch / Manjaro

```bash
sudo pacman -S git
```

### Debian / Ubuntu

```bash
sudo apt update
sudo apt install git
```

### Fedora

```bash
sudo dnf install git
```

### Verify

```bash
which git
git --version
```

## macOS

### Homebrew

```bash
brew install git
```

### Xcode Command Line Tools (alternative)

```bash
xcode-select --install
```

### Verify

```bash
git --version
which git
```

## Windows

### Git for Windows (recommended)

- Install “Git for Windows”
- It includes:
  - `git`
  - Git Bash
  - optional credential manager

Verify in **Git Bash** or PowerShell:

```bash
git --version
where git
```

### WSL (alternative)

If using WSL Ubuntu:

```bash
sudo apt update
sudo apt install git
git --version
```

## Update Git

### Linux

Use your package manager:

```bash
sudo pacman -Syu
sudo apt upgrade
sudo dnf upgrade
```

### macOS (Homebrew)

```bash
brew update
brew upgrade git
```

### Windows

Re-run Git for Windows installer (or use winget/choco if you installed via those).

## Troubleshooting

### “git: command not found”

- restart terminal
- confirm PATH includes Git
- verify with `which git` (macOS/Linux) or `where git` (Windows)

### Multiple Git installs

Check which binary is being used:

```bash
which git
where git
git --version
```

## Related Notes

- [[GitConfiguration]]
- [[SshKeysSetup]]
- [[git-config]]
