---
id: TcpAndUdp
aliases: []
tags: []
---

# TCP and UDP

The two primary transport layer protocols. TCP prioritizes reliability; UDP prioritizes speed.

## TCP (Transmission Control Protocol)

Connection-oriented. Establishes a connection before sending data.

### Three-way handshake

```
Client          Server
  | --- SYN --->   |
  | <-- SYN-ACK -- |
  | --- ACK --->   |
```

### Features

- Reliable delivery (retransmits lost packets)
- Ordered delivery
- Flow control (prevents overwhelming the receiver)
- Congestion control (backs off when network is busy)

### Common applications

| Port | Protocol | Service |
|---|---|---|
| 22 | TCP | SSH |
| 25 | TCP | SMTP |
| 80 | TCP | HTTP |
| 443 | TCP | HTTPS |
| 3306 | TCP | MySQL |
| 5432 | TCP | PostgreSQL |

## UDP (User Datagram Protocol)

Connectionless. Sends data without establishing a connection.

### Features

- No delivery guarantee
- No ordering
- No retransmission
- Low latency, minimal overhead

### Common applications

| Port | Protocol | Service |
|---|---|---|
| 53 | UDP | DNS |
| 67/68 | UDP | DHCP |
| 123 | UDP | NTP |
| 161 | UDP | SNMP |
| 1194 | UDP | OpenVPN |

## Comparison

| Feature | TCP | UDP |
|---|---|---|
| Connection | Required | None |
| Reliability | Guaranteed | Best-effort |
| Ordering | Preserved | Not preserved |
| Speed | Slower | Faster |
| Overhead | Higher | Lower |
| Use case | Web, email, SSH | DNS, streaming, gaming |

## Related Notes

- [[IpAddresses]]
- [[OsiModel]]
- [[TcpIpModel]]
