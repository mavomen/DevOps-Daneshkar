---
id: CommitMessageTemplate
aliases: []
tags: []
---

# Commit Message Template

Copy/paste template you can use for `commit.template` or your editor snippet.

## Template (Conventional-style)

```txt
type(scope): short summary (imperative)

Why:
-

What:
-

Testing:
-

Refs:
-
```

## Examples

```txt
feat(auth): add refresh token rotation

Why:
- Prevent long-lived sessions from being hijacked.

What:
- Rotate refresh token on use.
- Invalidate previous refresh token immediately.

Testing:
- Added unit tests for rotation.
- Verified login + refresh flows manually.

Refs:
- #412
```

## Git setup (optional)

Create `~/.config/git/commit-template.txt` and then:

```bash
git config --global commit.template ~/.config/git/commit-template.txt
```

Related:

- [[CommitMessageBestPractices]]
- [[CommitMessageTemplates]]
- [[GitConfiguration]]
