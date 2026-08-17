---
id: wireshark
aliases: []
tags: []
---

# Wireshark

GUI-based network protocol analyzer for deep packet inspection.

## Install

```bash
sudo apt install wireshark
```

## Basic usage

1. Select network interface
2. Click "Start capturing"
3. Apply display filters

## Display filters

| Filter | Meaning |
|---|---|
| `http` | HTTP traffic |
| `tcp.port == 443` | HTTPS traffic |
| `ip.src == 10.0.0.1` | Traffic from specific IP |
| `dns` | DNS queries |
| `tcp.flags.syn == 1` | SYN packets only |
| `http.response.code == 200` | Successful HTTP responses |

## tcpdump vs Wireshark

| | tcpdump | Wireshark |
|---|---|---|
| Interface | CLI | GUI |
| Use case | Quick capture, SSH sessions | Deep analysis, packet inspection |
| Filter syntax | BPF (Berkeley Packet Filter) | Wireshark display filters |
| Output | Text / pcap | Graphical packet tree |

## Related Notes

- [[Commands/tcpdump|tcpdump]]
- [[TcpAndUdp]]
- [[OsiModel]]
