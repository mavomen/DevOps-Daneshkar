---
id: git-clone
aliases: []
tags: []
---

# git clone

Copy an existing repository to a new local directory.

## Syntax

```bash
git clone <url> [<directory>]
git clone -b <branch> <url>
git clone --recurse-submodules <url>
git clone --depth <n> <url>
```

## Description

`git clone` creates a local copy of a remote repository, typically setting up a remote named `origin`.

## Common usage

### Clone to default folder name

```bash
git clone https://github.com/user/repo.git
```

### Clone into a specific directory name

```bash
git clone https://github.com/user/repo.git my-project
```

### Clone a specific branch

```bash
git clone -b main https://github.com/user/repo.git
```

### Clone with submodules

```bash
git clone --recurse-submodules https://github.com/user/repo.git
```

### Shallow clone (CI / quick checkouts)

```bash
git clone --depth 1 https://github.com/user/repo.git
```

## Related Notes

- [[Repository]]
- [[git-remote]]
- [[git-fetch]]
- [[git-submodule]]
