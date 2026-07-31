---
id: PermissionDenied
aliases: []
tags: []
---

# Permission Denied

Permission failures when reading/writing repository files or connecting to remotes.

## Symptoms

- “Permission denied” on push/pull
- filesystem permission errors in `.git/` or working tree
- SSH permission denied (publickey)

## Diagnosis

### Filesystem

```bash
ls -la
ls -la .git
```

### Remote URL + auth method

```bash
git remote -v
```

### SSH check (GitHub example)

```bash
ssh -T git@github.com
```

## Fixes

### Local filesystem

- ensure files are writable by you (avoid using `sudo git ...`)

### HTTPS auth

- refresh credentials / token in your credential manager
- ensure your token has correct scopes

### SSH auth

- ensure key exists and is loaded:

```bash
ssh-add -l
```

- confirm SSH key is added to your host account
- ensure remote URL is SSH, not HTTPS:

```bash
git remote -v
```

## Related Notes

- [[SshKeysSetup]]
- [[git-remote]]
- [[Troubleshooting/CommonProblems/AuthenticationFailures|AuthenticationFailures]]
