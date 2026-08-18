---
id: GrepRegexPatterns
aliases: []
tags: []
---

# Grep Regex Patterns

Using `grep` with regular expressions to filter and search text.

## Basic Syntax

```bash
grep 'pattern' file                         # Simple match
grep -i 'pattern' file                      # Case-insensitive
grep -n 'pattern' file                      # Show line numbers
grep -r 'pattern' directory                 # Recursive search
grep -c 'pattern' file                      # Count matches
grep -v 'pattern' file                      # Invert match
```

## Regex Patterns on /etc/passwd

### Exact String Match

```bash
grep devasc /etc/passwd
# devasc:x:900:900:DEVASC,,,:/home/devasc:/bin/bash
```

### Anchor: Start of Line (`^`)

```bash
grep '^root' /etc/passwd
# root:x:0:0:root:/root:/bin/bash
```

### Anchor: End of Line (`$`)

```bash
grep 'false$' /etc/passwd
# tss:x:106:114:TPM software stack,,,:/var/lib/tpm:/bin/false
# lightdm:x:107:117:Light Display Manager:/var/lib/lightdm:/bin/false
```

### Wildcard: Any Character (`.`)

```bash
grep 'd..m' /etc/passwd
# daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
# dnsmasq:x:109:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
```

### Character Class (`[ ]`)

```bash
grep '[8-9]' /etc/passwd                    # Lines containing 8 or 9
grep '[,]' /etc/passwd                      # Lines containing comma
```

### Zero or More (`*`)

```bash
grep 'new*' /etc/passwd                     # "ne", "new", "neww", etc.
```

## Common Patterns

| Pattern | Meaning | Example |
|---------|---------|---------|
| `^root` | Lines starting with "root" | `grep '^root' /etc/passwd` |
| `bash$` | Lines ending with "bash" | `grep 'bash$' /etc/passwd` |
| `[0-9]` | Any digit | `grep '[0-9]' file` |
| `[^a-z]` | Not lowercase | `grep '[^a-z]' file` |
| `.*` | Any characters | `grep 'root.*bash' file` |
| `\<word\>` | Whole word | `grep '\<root\>' file` |

## Related Notes

- [[UserAccountInvestigation]] — Investigating user accounts
- [[AuthenticationLogs]] — Log analysis
