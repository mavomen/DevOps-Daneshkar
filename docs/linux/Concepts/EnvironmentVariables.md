---
id: EnvironmentVariables
aliases: []
tags: []
---

# Environment Variables

Shell variables that affect process behavior.

## Key Variables

| Variable | Purpose | Example |
|----------|---------|---------|
| `PATH` | Directories to search for executables | `/usr/bin:/usr/local/bin` |
| `HOME` | User home directory | `/home/mava` |
| `USER` | Current username | `mava` |
| `SHELL` | Current shell | `/bin/zsh` |
| `LANG` | Locale/language | `en_US.UTF-8` |
| `EDITOR` | Default text editor | `vim` |
| `PS1` | Shell prompt | `\u@\h:\w$ ` |
| `HOME` | Home directory | `/home/user` |
| `TMPDIR` | Temp directory | `/tmp` |

## Commands

```bash
echo $PATH                                  # Print variable
env                                         # All environment variables
export MY_VAR="hello"                       # Set for child processes
MY_VAR="hello"                              # Set for current shell only
unset MY_VAR                                # Remove variable
```

## Persistent Configuration

| File | Scope | When Loaded |
|------|-------|-------------|
| `~/.bashrc` or `~/.zshrc` | Current user | Interactive shell |
| `~/.bash_profile` or `~/.zsh_profile` | Current user | Login shell |
| `/etc/profile` | All users | Login shell |
| `/etc/environment` | All users | All sessions |
| `/etc/profile.d/*.sh` | All users | Login shell |

## PATH Management

```bash
echo $PATH | tr ':' '\n'                    # View PATH entries
export PATH="$PATH:/opt/myapp/bin"          # Add to PATH
```

## Related Notes

- [[ShellBasics]] — Shell basics
- [[EtcEnvironment]] — /etc/environment config
- [[ScriptingStandards]] — Scripting best practices
