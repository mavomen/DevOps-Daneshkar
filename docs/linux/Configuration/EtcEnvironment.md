---
id: EtcEnvironment
aliases: []
tags: []
---

# /etc/environment — System-wide Environment Variables

Persistent environment variables for all users and services.

## Format

```
PATH="/usr/local/bin:/usr/bin:/bin"
JAVA_HOME="/usr/lib/jvm/java-17"
APP_ENV="production"
```

## Key Files

| File | Scope | Purpose |
|------|-------|---------|
| `/etc/environment` | All users | System-wide vars |
| `/etc/profile` | All users (login shells) | Profile setup |
| `/etc/profile.d/*.sh` | All users (login shells) | Modular profile scripts |
| `~/.profile` | Current user | User profile |
| `~/.bashrc` | Current user (interactive) | Shell aliases, functions |
| `~/.bash_profile` | Current user (login) | Login shell setup |

## View & Set

```bash
echo $PATH                                 # View variable
echo $HOME                                 # Home directory
env | sort                                 # All environment variables
export MY_VAR="value"                      # Set for current session
```

## Make Persistent

```bash
echo 'export MY_VAR="value"' >> ~/.bashrc   # User-level
echo 'MY_VAR="value"' | sudo tee /etc/environment  # System-wide
```

## Related Notes

- [[ShellBasics]] — Shell environment
- [[EnvironmentVariables]] — Variables concept
- [[SudoConfiguration]] — Sudo and environment
