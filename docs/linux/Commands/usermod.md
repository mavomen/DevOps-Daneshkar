---
id: usermod
aliases: []
tags: []
---

# usermod

Modify a user account.

## Syntax

```bash
usermod [options] username
```

## Common Usage

```bash
usermod -aG docker alice
```

```bash
usermod -s /bin/zsh alice
```

```bash
usermod -L alice
```

## Tips

- -aG append to group (without -a, replaces groups), -L lock, -U unlock

## Related Notes

- [[UsersAndGroups]]
