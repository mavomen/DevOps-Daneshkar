---
id: ProcessAnalysis
aliases: []
tags: []
---

# Process Analysis — Troubleshooting

Investigating process behavior and resource usage.

## Find Processes

```bash
ps aux | grep nginx                        # By name
ps -ef | grep -v grep | grep java         # By command
pgrep -la nginx                            # Quick search
pidof nginx                                # Get PID
```

## Resource Usage

```bash
top -bn1 | head -20                        # CPU/memory overview
top -p PID                                 # Monitor specific PID
ps -eo pid,ppid,user,%cpu,%mem,rss,vsz,cmd --sort=-%cpu | head  # Top CPU
ps -eo pid,ppid,user,%cpu,%mem,rss,vsz,cmd --sort=-%mem | head  # Top RAM
```

## Process Tree

```bash
pstree -p                                  # All processes
pstree -p PID                              # Subtree of PID
ps -ef --forest                            # Forest view
```

## Trace System Calls

```bash
strace -p PID                              # Attach to running
strace -f command                          # Trace new command
strace -e trace=network command            # Network calls only
```

## Kill Process

```bash
kill PID                                   # SIGTERM (graceful)
kill -9 PID                                # SIGKILL (force)
killall nginx                              # By name
pkill -f "python app.py"                   # By pattern
```

## Background vs Foreground

```bash
jobs                                       # List background jobs
bg %1                                      # Resume job 1 in background
fg %1                                      # Bring to foreground
nohup command &                            # Detach from terminal
```

## Related Notes

- [[ProcessManagement]] — Process concepts
- [[SignalsAndTraps]] — Signal reference
- [[SystemStatus]] — System monitoring
- [[kill]] — Kill command
