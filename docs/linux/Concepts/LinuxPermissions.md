---
id: LinuxPermissions
aliases: []
tags: []
---

# Linux Permissions

Every file and directory has an owner, a group, and a set of permission bits.

## Permission Bits

| Bit | File | Directory |
|-----|------|-----------|
| `r` (4) | Read content | List contents |
| `w` (2) | Modify content | Create/delete files inside |
| `x` (1) | Execute as program | Enter (cd into) directory |

## Notation

```bash
-rwxr-xr-- 1 user group 4096 Jan 1 00:00 file.txt
│└┬┘└┬┘└┬┘
│ │   │   └── Other (r--)
│ │   └────── Group (r-x)
│ └────────── Owner (rwx)
└──────────── Type (- = file, d = directory)
```

## Octal Reference

| Octal | Binary | Permissions |
|-------|--------|-------------|
| 7 | 111 | rwx |
| 6 | 110 | rw- |
| 5 | 101 | r-x |
| 4 | 100 | r-- |
| 0 | 000 | --- |

Common modes: `755` (dirs), `644` (files), `700` (private), `600` (secrets)

## Commands

```bash
chmod 755 file                             # Set permissions
chmod u+x script.sh                        # Add execute for owner
chmod -R 644 /path/                        # Recursive
chown user:group file                      # Change owner:group
chown -R www-data:www-data /var/www        # Recursive ownership
```

## Special Permissions

| Permission | Octal | Effect |
|------------|-------|--------|
| SUID | 4000 | Run as file owner |
| SGID | 2000 | Run as group / inherit group |
| Sticky bit | 1000 | Only owner can delete |

```bash
chmod u+s /usr/bin/passwd                  # SUID
chmod g+s /shared/                         # SGID
chmod +t /tmp/                             # Sticky bit
```

## umask

Default permissions for new files/dirs:

```bash
umask                                      # Show current umask
umask 022                                  # Files: 644, Dirs: 755
```

## Related Notes

- [[FilesystemHierarchy]] — Directory structure
- [[chmod]] — chmod command
- [[chown]] — chown command
- [[SecurityHardening]] — Security best practices
