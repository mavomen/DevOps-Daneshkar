---
id: git-credential
aliases: []
tags: []
---

# git credential

Interact with Git’s credential subsystem (helpers) used for HTTPS auth.

## Syntax

```bash
git credential fill
git credential approve
git credential reject
```

## Description

`git credential` is a low-level interface Git uses to ask credential helpers for usernames/passwords/tokens for HTTPS remotes.

You usually do not run it daily, but it’s useful for debugging auth issues.

Credential helpers are configured via:

```bash
git config --global credential.helper <helper>
```

Related: [[GitConfiguration]], [[AuthenticationFailures]]

## Basic Usage (Debugging)

### Fill (ask helper for creds)

```bash
printf "protocol=https\nhost=github.com\n\n" | git credential fill
```

Git prints something like:

```txt
protocol=https
host=github.com
username=...
password=...
```

### Reject (remove creds from helper)

```bash
printf "protocol=https\nhost=github.com\nusername=...\n\n" | git credential reject
```

> In practice, removing credentials is often done via your OS credential manager UI.

## Common Helpers

Examples (vary by OS and setup):

```bash
git config --global credential.helper cache
git config --global credential.helper store
git config --global credential.helper manager-core
```

## Security notes

- `store` saves tokens in plaintext — avoid unless you understand the risk.
- Prefer OS keychains / credential managers when possible.

## Related Notes

- [[GitConfiguration]]
- [[SshKeysSetup]] (SSH alternative to HTTPS)
- [[Troubleshooting/CommonProblems/AuthenticationFailures|AuthenticationFailures]]
- [[git-remote]]
