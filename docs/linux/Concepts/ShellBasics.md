---
id: ShellBasics
aliases: []
tags: []
---

# Shell Basics

The shell interprets commands and provides an interface to the operating system.

## Popular Shells

| Shell | Path | Features |
|-------|------|----------|
| Bash | `/bin/bash` | Default on most distros, POSIX-compatible |
| Zsh | `/bin/zsh` | Autocomplete, themes, plugins |
| Fish | `/usr/bin/fish` | User-friendly, syntax highlighting |
| Sh | `/bin/sh` | Minimal POSIX shell |

## Shell Expansion

```bash
echo $HOME                                  # Variable expansion
echo $(date)                                # Command substitution
echo ~                                      # Home directory
echo ${VAR:-default}                        # Default value
echo {a,b,c}                                # Brace expansion
echo file{1..5}.txt                         # Range expansion
```

## Aliases & History

```bash
alias ll='ls -la'                           # Create alias
alias -p                                    # List aliases
history                                     # Command history
history | grep docker                       # Search history
!!                                          # Re-run last command
!grep                                       # Re-run last grep command
```

## Redirection & Pipes

```bash
command > file                              # stdout to file (overwrite)
command >> file                             # stdout to file (append)
command 2> error.log                        # stderr to file
command &> all.log                          # stdout + stderr to file
command1 | command2                         # Pipe stdout to next command
command < input.txt                         # stdin from file
command << EOF                              # Here document
content
EOF
```

## Related Notes

- [[EnvironmentVariables]] — Environment and PATH
- [[TextProcessing]] — Text tools (grep, sed, awk)
- [[GrepRegexPatterns]] — grep patterns
