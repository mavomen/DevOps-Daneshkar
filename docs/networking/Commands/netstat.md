---
id: netstat
aliases: []
tags: []
---

# netstat

Display network connections, routing tables, and port usage. Largely replaced by `ss`.

## Common commands

```bash
# Show all listening ports
netstat -tlnp

# Show all connections
netstat -tunap

# Show only listening TCP
netstat -tlnp

# Show routing table
netstat -r

# Show network interface statistics
netstat -i
```

## Options

| Option | Purpose |
|---|---|
| `-t` | TCP |
| `-u` | UDP |
| `-l` | Listening only |
| `-n` | No DNS resolution |
| `-p` | Show PID/program name |
| `-a` | All (listening + established) |
| `-r` | Routing table |

## Notes

- `netstat` is deprecated. Use `ss` instead.
- `ss` is faster and provides more socket information.

## Related Notes

- [[Commands/ss|ss]]
- [[TcpAndUdp]]
- [[Firewall]]
