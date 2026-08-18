---
id: ScriptingStandards
aliases: []
tags: []
---

# Scripting Standards — Best Practices

Writing robust, maintainable shell scripts.

## Script Template

```bash
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# Script: myapp.sh
# Description: Brief description
# Usage: ./myapp.sh [options]

LOGFILE="/var/log/myapp.log"
readonly SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"

log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $*" | tee -a "$LOGFILE"
}

die() {
    log "ERROR: $*" >&2
    exit 1
}

main() {
    log "Starting..."
    # Logic here
    log "Done."
}

main "$@"
```

## Key Principles

| Rule | Why |
|------|-----|
| `set -euo pipefail` | Fail on errors, undefined vars, pipe failures |
| Quote variables | Prevent word splitting (`"$var"`) |
| Use `[[ ]]` | Better than `[ ]` (no word splitting) |
| Check exit codes | `command \|\| die "Failed"` |
| Avoid `eval` | Security risk |
| Use `mktemp` | Never hardcode temp paths |

## Input Validation

```bash
[[ -f "$1" ]] || die "File not found: $1"
[[ -z "${NAME:-}" ]] && die "NAME is required"
[[ "$PORT" =~ ^[0-9]+$ ]] || die "PORT must be numeric"
```

## Error Handling

```bash
trap 'cleanup' EXIT
trap 'die "Interrupted" ' INT TERM

cleanup() {
    rm -f "$TEMP_FILE" 2>/dev/null
}
```

## Related Notes

- [[ShellBasics]] — Shell fundamentals
- [[ProcessManagement]] — Process control
- [[LogSystem]] — Logging
