---
id: FirstCommit
aliases: []
tags: []
---

# First Commit

Your first commit creates the initial snapshot of the project and sets a clean baseline for collaboration.

## Typical first commit contents

- `README.md`
- `.gitignore` (see [[GitIgnorePatterns]])
- basic project skeleton (`src/`, `docs/`, etc.)

## Steps

1. Verify status

```bash
git status -sb
```

2. Stage files

```bash
git add .
```

3. Commit

```bash
git commit -m "chore: initial commit"
```

4. (Optional) push to remote

```bash
git push -u origin main
```

## Notes

- Prefer a meaningful initial message (not just “init”).
- If you need an empty commit (rare), you can do:

```bash
git commit --allow-empty -m "chore: initial commit"
```

## Related Notes

- [[git-add]]
- [[git-commit]]
- [[git-push]]
- [[RepositoryInitialization]]
