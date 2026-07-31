---
id: RepositoryInitialization
aliases: []
tags: []
---

# Repository Initialization

A practical checklist for creating a new Git repository correctly from day one.

## Prereqs (once per machine)

- [[GitInstallation]]
- [[GitConfiguration]]
- (Optional) [[SshKeysSetup]]

## Initialize a new repository

```bash
mkdir my-project
cd my-project
git init --initial-branch=main
```

## Add essential starter files

Typical minimum:

- `README.md`
- `.gitignore` (see [[GitIgnorePatterns]])

Example:

```bash
printf "# My Project\n" > README.md
printf "node_modules/\n.env\n" > .gitignore
```

## Make the first commit

See: [[FirstCommit]]

## Connect a remote (optional but recommended)

```bash
git remote add origin <url>
git remote -v
```

## Push to remote

```bash
git push -u origin main
```

## Related Notes

- [[git-init]]
- [[git-remote]]
- [[git-push]]
- [[FirstCommit]]
