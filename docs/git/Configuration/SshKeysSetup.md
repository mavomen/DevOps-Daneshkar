---
id: ShKeysSetup
aliases: []
tags: []
---

# SSH Keys Setup

Set up SSH keys to authenticate to Git hosting services (GitHub/GitLab/etc.) without typing passwords/tokens repeatedly.

## Suggested Aliases (optional)

- `SSH Keys Setup`
- `Ssh Keys Setup`

## Generate a Key (Ed25519)

```bash
ssh-keygen -t ed25519 -C "you@example.com"
```

Recommended prompts:

- file: default (`~/.ssh/id_ed25519`)
- passphrase: recommended (use an agent)

## Start SSH Agent + Add Key

### Linux/macOS (typical)

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Windows

- Git Bash usually supports `ssh-agent`
- Or rely on Windows OpenSSH agent

Verify keys loaded:

```bash
ssh-add -l
```

## Add Public Key to Host

Print public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy it into your Git hosting account SSH keys.

## Test Connection

GitHub example:

```bash
ssh -T git@github.com
```

GitLab example:

```bash
ssh -T git@gitlab.com
```

## Use SSH Remote URLs

Example:

```bash
git remote set-url origin git@github.com:USER/REPO.git
git remote -v
```

See: [[git-remote]]

## Multiple Keys (Optional)

Create `~/.ssh/config`:

```sshconfig
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
```

For work/personal separation:

```sshconfig
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work
  IdentitiesOnly yes
```

Then use:

```bash
git remote set-url origin git@github-work:ORG/REPO.git
```

## Troubleshooting

### “Permission denied (publickey)”

- confirm key is loaded: `ssh-add -l`
- confirm remote URL is SSH: `git remote -v`
- confirm your public key is added to the hosting service
- run verbose SSH:

```bash
ssh -vT git@github.com
```

### Wrong key used

Use `~/.ssh/config` with `IdentitiesOnly yes`.

## Related Notes

- [[GitConfiguration]]
- [[git-clone]]
- [[git-push]]
- [[git-remote]]
