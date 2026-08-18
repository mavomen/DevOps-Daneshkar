---
id: useradd
aliases: []
tags: []
---

# useradd

Create a new user account.

## Syntax

```bash
useradd [options] username
```

## Common Usage

```bash
useradd -m -s /bin/bash newuser
```

```bash
useradd -m -G docker newuser
```

```bash
useradd -m -d /opt/app appuser -s /sbin/nologin
```

## Tips

- -m creates home dir, -s sets shell, -G adds to supplementary groups

## Related Notes

- [[UsersAndGroups]]
