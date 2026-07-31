---
id: RemoteSyntax
aliases: []
tags: []
---

# Remote Syntax

How remote names, remote-tracking branches, and refspecs are written.

## Remote name basics

- `origin` is just a conventional remote name
- `upstream` is commonly used for the canonical repo in fork workflows

See: [[UpstreamAndOrigin]]

List remotes:

```bash
git remote -v
```

## Remote-tracking branches

Remote-tracking branches look like:

- `origin/main`
- `origin/feature/x`

They are updated by [[git-fetch]].

## Common pull syntax

```bash
git pull origin main
git pull --rebase origin main
```

## Common push syntax

```bash
git push origin main
git push -u origin feature/x
```

## Refspec form

Push local branch to remote branch:

```bash
git push origin local-branch:remote-branch
```

Delete remote branch:

```bash
git push origin --delete remote-branch
# or
git push origin :remote-branch
```

## Related Notes

- [[git-remote]]
- [[git-fetch]]
- [[git-pull]]
- [[git-push]]
