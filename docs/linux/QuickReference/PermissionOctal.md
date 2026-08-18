---
id: PermissionOctal
aliases: []
tags: []
---

# Permission Octal Numbers — Quick Reference

## Octal to Symbolic

| Octal | Symbolic | Meaning |
|-------|----------|---------|
| 0 | `---` | No permission |
| 1 | `--x` | Execute |
| 2 | `-w-` | Write |
| 3 | `-wx` | Write + Execute |
| 4 | `r--` | Read |
| 5 | `r-x` | Read + Execute |
| 6 | `rw-` | Read + Write |
| 7 | `rwx` | Read + Write + Execute |

## Common Permissions

| Octal | Use Case |
|-------|----------|
| `755` | Executables, directories |
| `644` | Regular files |
| `600` | Private files (ssh keys) |
| `700` | Private directories (ssh) |
| `444` | Read-only |
| `666` | World read/write (avoid!) |
| `777` | Full access (avoid!) |

## Quick Calc

```
User:   r=4 + w=2 + x=1
Group:  r=4 + w=2 + x=1
Other:  r=4 + w=2 + x=1

Example: rwxr-xr-- = 754
```

## Related Notes

- [[LinuxPermissions]] — Full concept
- [[chmod]] — chmod command
- [[chown]] — Ownership
