---
id: nmap
aliases: []
tags: []
---

# nmap

Network exploration and port scanning tool.

## Basic usage

```bash
# Scan a host
nmap 192.168.1.20

# Scan specific ports
nmap -p 22,80,443 192.168.1.20

# Scan all ports
nmap -p- 192.168.1.20

# Service/version detection
nmap -sV 192.168.1.20

# OS detection
nmap -O 192.168.1.20

# Scan a subnet
nmap 192.168.1.0/24

# Fast scan (top 100 ports)
nmap -F 192.168.1.20

# Scan without DNS resolution
nmap -n 192.168.1.20

# Aggressive scan (OS + version + scripts)
nmap -A 192.168.1.20
```

## Scan types

| Type | Flag | Description |
|---|---|---|
| TCP SYN | `-sS` | Stealth scan (default, requires root) |
| TCP Connect | `-sT` | Full TCP connection |
| UDP | `-sU` | Scan UDP ports (slow) |
| ICMP | `-sn` | Ping sweep (host discovery) |

## Common port ranges

| Range | Name |
|---|---|
| 1-1023 | Well-known |
| 1024-49151 | Registered |
| 49152-65535 | Dynamic/Ephemeral |

## Notes

- Port scanning without authorization may be illegal.
- Use only on networks you own or have permission to test.
- `nmap -sV` is the most useful single scan — tells you what's running.

## Related Notes

- [[Commands/tcpdump|tcpdump]]
- [[TcpAndUdp]]
- [[Firewall]]
