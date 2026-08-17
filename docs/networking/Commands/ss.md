---
id: ss
aliases: []
tags: []
---

# ss

Socket statistics. Modern replacement for `netstat`. Faster and more detailed.

## Common commands

```bash
# Show all listening TCP sockets
ss -tlnp

# Show all established TCP connections
ss -tanp

# Show all sockets (TCP + UDP)
ss -tunap

# Show sockets for a specific process
ss -tlnp | grep nginx

# Show socket memory usage
ss -tlnm

# Show internal TCP information
ss -ti
```

## Options

| Option | Purpose |
|---|---|
| `-t` | TCP |
| `-u` | UDP |
| `-l` | Listening |
| `-n` | No DNS resolution |
| `-p` | Show process |
| `-a` | All sockets |
| `-m` | Show memory usage |
| `-i` | Show internal TCP info (RTT, cwnd) |
| `-s` | Summary statistics |

## Output columns

| Column | Meaning |
|---|---|
| State | LISTEN, ESTAB, TIME-WAIT, etc. |
| Recv-Q | Data waiting to be read |
| Send-Q | Data waiting to be sent |
| Local Address:Port | Socket bind address |
| Peer Address:Port | Remote address |

## Related Notes

- [[Commands/netstat|netstat]]
- [[TcpAndUdp]]
- [[Commands/tcpdump|tcpdump]]
