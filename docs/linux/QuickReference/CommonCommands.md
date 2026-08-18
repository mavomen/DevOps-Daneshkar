---
id: CommonCommands
aliases: []
tags: []
---

# Linux Common Commands — Quick Reference

## File Operations

| Command | Description |
|---------|-------------|
| `ls -la` | List all files with details |
| `cp -r src/ dest/` | Copy directory recursively |
| `mv old new` | Move/rename |
| `rm -rf dir/` | Remove directory (careful!) |
| `mkdir -p a/b/c` | Create nested dirs |
| `touch file` | Create empty file |
| `find . -name "*.py"` | Search by name |
| `ln -s target link` | Create symlink |

## Text Processing

| Command | Description |
|---------|-------------|
| `grep -rn "pattern" .` | Search recursively |
| `sed 's/old/new/g' file` | Replace text |
| `awk '{print $1}' file` | Print column |
| `sort -u file` | Sort unique |
| `cut -d: -f1 file` | Extract fields |
| `head -20 file` | First 20 lines |
| `tail -f log` | Follow log |
| `wc -l file` | Count lines |

## Process Management

| Command | Description |
|---------|-------------|
| `ps aux \| grep NAME` | Find process |
| `top` | Interactive monitor |
| `kill PID` | Terminate (SIGTERM) |
| `kill -9 PID` | Force kill |
| `nohup cmd &` | Run in background |
| `systemctl status svc` | Service status |
| `systemctl restart svc` | Restart service |

## Disk & System

| Command | Description |
|---------|-------------|
| `df -h` | Disk usage |
| `du -sh dir/` | Directory size |
| `free -h` | Memory usage |
| `uname -a` | System info |
| `uptime` | Load and uptime |
| `whoami` | Current user |
| `id` | User and groups |
| `last -10` | Last logins |

## Network

| Command | Description |
|---------|-------------|
| `ip addr show` | IP addresses |
| `ss -tlnp` | Listening ports |
| `ping -c 4 host` | Test connectivity |
| `curl -I url` | HTTP headers |
| `dig example.com` | DNS query |
| `traceroute host` | Route trace |

## Related Notes

- [[FilesystemHierarchy]] — FS layout
- [[LinuxPermissions]] — Permissions
- [[ShellBasics]] — Shell usage
