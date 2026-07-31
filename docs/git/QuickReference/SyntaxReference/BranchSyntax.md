---
id: BranchSyntax
aliases: []
tags: []
---

# Branch Syntax

Common branch naming patterns and branch reference syntax.

## Naming patterns (recommended)

- `feature/<name>`
- `fix/<name>`
- `hotfix/<name>`
- `release/<version>`
- `chore/<name>`

See: [[BranchNamingConventions]]

## Branch references

Examples:

- local branches: `main`, `feature/x`
- remote-tracking branches: `origin/main`, `origin/feature/x`

Examples:

```bash
git log origin/main --oneline
git diff main..origin/main
```

## Creating branches

```bash
git switch -c feature/x
git switch -c feature/x main
git branch feature/x
```

## Deleting branches

```bash
git branch -d feature/x
git push origin --delete feature/x
```

## Related Notes

- [[git-branch]]
- [[git-switch]]
- [[Remote]]
- [[UpstreamAndOrigin]]
