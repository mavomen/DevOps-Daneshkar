---
id: GitHooks
aliases: []
tags: []
---

# Git Hooks

Git hooks are scripts Git runs automatically at specific points (pre-commit, commit-msg, pre-push, etc.).

## Suggested Aliases (optional)

- `Git Hooks`

## Where Hooks Live

Per-repository hooks:

- `.git/hooks/`

List sample hooks:

```bash
ls .git/hooks
```

Enable a hook by:

1. creating the hook file (no extension)
2. making it executable

Example:

```bash
chmod +x .git/hooks/pre-commit
```

## Common Hooks

| Hook            | Runs when                | Typical use              |
| --------------- | ------------------------ | ------------------------ |
| `pre-commit`    | before commit is created | lint/format/tests        |
| `commit-msg`    | validate commit message  | conventional commits     |
| `pre-push`      | before pushing           | run tests, block secrets |
| `post-checkout` | after checkout/switch    | install deps, regenerate |
| `post-merge`    | after merge              | update deps              |

## Example: pre-commit (run tests)

Create `.git/hooks/pre-commit`:

```bash
#!/usr/bin/env bash
set -e

echo "Running tests..."
npm test
```

Make executable:

```bash
chmod +x .git/hooks/pre-commit
```

## Example: commit-msg (simple conventional format)

`.git/hooks/commit-msg`:

```bash
#!/usr/bin/env bash
set -e

msg_file="$1"
regex='^(feat|fix|docs|style|refactor|perf|test|chore)(\(.+\))?: .+'

if ! grep -qE "$regex" "$msg_file"; then
  echo "Invalid commit message."
  echo "Expected: type(scope): message"
  exit 1
fi
```

## Sharing Hooks with a Team (Recommended)

The `.git/hooks` folder is not committed. For shared hooks:

1. create a tracked folder like `githooks/`
2. point Git to it:

```bash
git config core.hooksPath githooks
```

Then commit `githooks/pre-commit`, etc.

## Troubleshooting

### Hook not running

- ensure executable: `chmod +x`
- ensure correct filename (no extension)
- ensure `core.hooksPath` isn’t pointing elsewhere:

```bash
git config --get core.hooksPath
```

## Related Notes

- [[GitConfiguration]]
- [[CiCdIntegration]]
- [[git-commit]]
