---
id: ProcessManagement
aliases: []
tags: []
---

# Process Management

Linux processes, their lifecycle, signals, and job control.

## Process States

| State | Meaning |
|-------|---------|
| `R` | Running or runnable |
| `S` | Sleeping (interruptible) |
| `D` | Sleeping (uninterruptible, I/O) |
| `T` | Stopped |
| `Z` | Zombie (terminated, not yet reaped) |
| `I` | Idle (kernel thread) |

## Process Hierarchy

```
systemd (PID 1)
├── sshd
│   └── bash
│       └── python app.py
├── nginx
│   ├── master
│   └── worker
```

## Signals

| Signal | Number | Default Action | Use Case |
|--------|--------|----------------|----------|
| `SIGHUP` | 1 | Terminate | Reload config |
| `SIGINT` | 2 | Terminate | Ctrl+C |
| `SIGQUIT` | 3 | Core dump | Ctrl+\ |
| `SIGKILL` | 9 | Terminate (forced) | Kill unresponsive |
| `SIGTERM` | 15 | Terminate (graceful) | Default kill |
| `SIGSTOP` | 19 | Stop | Pause process |
| `SIGCONT` | 18 | Continue | Resume process |
| `SIGUSR1` | 10 | Varies | App-specific |
| `SIGUSR2` | 12 | Varies | App-specific |

## Job Control

```bash
jobs                                        # List background jobs
bg %1                                       # Resume job in background
fg %1                                       # Bring job to foreground
Ctrl+Z                                      # Suspend current job
nohup command &                             # Run immune to hangup
```

## Related Notes

- [[SignalsAndTraps]] — Signals in scripts
- [[ps]] — Process listing
- [[top]] — Real-time process monitor
- [[kill]] — Sending signals
