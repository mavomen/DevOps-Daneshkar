---
id: tcpdump
aliases: []
tags: []
---

# tcpdump

Command-line packet capture tool. Captures network traffic flowing through an interface.

## Syntax

```bash
tcpdump [OPTIONS] [FILTER]
```

## Common examples

```bash
# Capture on default interface
sudo tcpdump

# Capture on specific interface
sudo tcpdump -i eth0

# Capture on all interfaces
sudo tcpdump -i any

# Capture only port 80
sudo tcpdump port 80

# Capture only traffic to/from a host
sudo tcpdump host 192.168.1.20

# Capture only TCP SYN packets
sudo tcpdump 'tcp[tcpflags] & (tcp-syn) != 0'

# Write to file (pcap format)
sudo tcpdump -i eth0 -w capture.pcap

# Read from pcap file
tcpdump -r capture.pcap

# Limit to 100 packets
sudo tcpdump -c 100

# Don't resolve hostnames
sudo tcpdump -n
```

## Display options

| Option | Purpose |
|---|---|
| `-i` | Interface |
| `-n` | No DNS resolution |
| `-v` / `-vv` | Verbose output |
| `-c` | Packet count limit |
| `-w` | Write to file |
| `-r` | Read from file |
| `-X` | Show packet contents (hex + ASCII) |

## Common filters

| Filter | Meaning |
|---|---|
| `port 80` | HTTP traffic |
| `host 10.0.0.1` | Traffic to/from specific host |
| `net 192.168.1.0/24` | Traffic to/from subnet |
| `tcp` | TCP only |
| `udp` | UDP only |
| `icmp` | ICMP only |

## Related Notes

- [[Commands/wireshark|wireshark]]
- [[TcpAndUdp]]
- [[OsiModel]]
