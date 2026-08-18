---
id: SignalsAndTraps
aliases: []
tags: []
---

# Signals & Traps

Signals are software interrupts sent to processes. Traps catch them in scripts.

## Common Signals

| Signal | Number | Default Action | Use Case |
|--------|--------|----------------|----------|
| `SIGHUP` | 1 | Terminate | Reload configuration |
| `SIGINT` | 2 | Terminate | Interrupt (Ctrl+C) |
| `SIGQUIT` | 3 | Core dump | Quit (Ctrl+\) |
| `SIGKILL` | 9 | Kill (forced) | Cannot be caught |
| `SIGTERM` | 15 | Terminate | Graceful shutdown |
| `SIGUSR1` | 10 | Varies | App-defined |
| `SIGUSR2` | 12 | Varies | App-defined |
| `SIGSTOP` | 19 | Stop | Pause (cannot be caught) |
| `SIGCONT` | 18 | Continue | Resume |

## Send Signals

```bash
kill -9 1234                                # Force kill PID 1234
kill -15 1234                               # Graceful terminate
kill -HUP 1234                              # Reload config
killall nginx                               # Kill by name
pkill -f "python app.py"                    # Kill by pattern
```

## Trap in Scripts

```bash
#!/bin/bash

cleanup() {
    echo "Cleaning up..."
    rm -f /tmp/lockfile
    exit 0
}

trap cleanup EXIT INT TERM

# ... script logic ...

# Script exits normally or on signal -> cleanup runs
```

## Common Patterns

```bash
trap '' INT                                 # Ignore SIGINT
trap - INT                                  # Reset SIGINT to default
trap 'echo "Error on line $LINENO"' ERR     # On error
trap '' HUP                                  # Ignore hangup (for nohup alternative)
```

## Related Notes

- [[ProcessManagement]] — Process lifecycle
- [[kill]] — kill command
- [[nohup]] — Running immune to hangup
