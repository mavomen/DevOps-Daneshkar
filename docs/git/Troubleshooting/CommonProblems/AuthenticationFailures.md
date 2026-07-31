---
id: AuthenticationFailures
aliases: []
tags: []
---

# Authentication Failures

Auth failures are usually wrong credentials, wrong remote URL type, expired tokens, or missing SSH keys.

## Symptoms

- HTTPS: “Authentication failed”
- SSH: “Permission denied (publickey)”
- Push rejected due to permission/access

## Diagnosis

```bash
git remote -v
```

### If using SSH

```bash
ssh -T git@github.com
ssh-add -l
```

### If using HTTPS

- verify your credential helper:

```bash
git config --global credential.helper
```

## Fixes

### Switch to SSH (common fix)

```bash
git remote set-url origin git@github.com:USER/REPO.git
```

Then ensure key setup: [[SshKeysSetup]]

### Refresh tokens (HTTPS)

- regenerate token in your host
- remove old stored credentials in your OS credential manager
- retry `git push`

## Related Notes

- [[SshKeysSetup]]
- [[GitConfiguration]]
- [[git-remote]]
- [[git-push]]
