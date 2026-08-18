---
id: SignalNumbers
aliases: []
tags: []
---

# Signal Numbers — Quick Reference

## Common Signals

| Signal | Number | Default Action | Purpose |
|--------|--------|----------------|---------|
| `SIGHUP` | 1 | Terminate | Hangup, reload config |
| `SIGINT` | 2 | Terminate | Interrupt (Ctrl+C) |
| `SIGQUIT` | 3 | Core dump | Quit (Ctrl+\) |
| `SIGKILL` | 9 | Terminate | Force kill (can't catch) |
| `SIGTERM` | 15 | Terminate | Graceful termination |
| `SIGSTOP` | 19 | Stop | Pause (can't catch) |
| `SIGCONT` | 18 | Continue | Resume stopped process |
| `SIGUSR1` | 10 | Terminate | User-defined 1 |
| `SIGUSR2` | 12 | Terminate | User-defined 2 |

## Usage

```bash
kill -SIGTERM PID                          # By name
kill -15 PID                               # By number
kill -9 PID                                # Force kill
killall -HUP nginx                         # Send to all by name
pkill -f "pattern"                         # By pattern
```

## Catching Signals

```bash
trap 'echo "Caught INT"' INT              # Catch Ctrl+C
trap '' INT                               # Ignore INT
trap - INT                                # Reset handler
trap 'cleanup; exit' EXIT TERM INT        # Cleanup on exit
```

## Related Notes

- [[SignalsAndTraps]] — Full signal guide
- [[kill]] — Kill command
- [[ProcessManagement]] — Process concepts
