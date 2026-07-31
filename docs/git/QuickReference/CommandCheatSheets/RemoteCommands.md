---
id: RemoteCommands
aliases: []
tags: []
---

# Remote Commands (Cheat Sheet)

Common remote operations: configure remotes, fetch, pull, push.

## Remotes

```bash
git remote
git remote -v
git remote show origin

git remote add origin <url>
git remote set-url origin <url>
git remote rename <old> <new>
git remote remove <name>
```

## Fetch

```bash
git fetch
git fetch origin
git fetch --all
git fetch --prune
git fetch --tags
```

## Pull

```bash
git pull
git pull origin main
git pull --rebase
git pull --ff-only
```

## Push

```bash
git push
git push origin main
git push -u origin <branch>

git push origin --delete <branch>
git push origin --tags
```

## Force push (careful)

```bash
git push --force-with-lease origin <branch>
# avoid: git push --force
```

## Related Notes

- [[git-remote]]
- [[git-fetch]]
- [[git-pull]]
- [[git-push]]
- [[UpstreamAndOrigin]]
