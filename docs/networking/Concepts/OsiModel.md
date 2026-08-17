---
id: OsiModel
aliases: []
tags: []
---

# OSI Model

The Open Systems Interconnection model is a 7-layer conceptual framework for how network communication works.

## The 7 layers

| Layer | Name | Function | Examples |
|---|---|---|---|
| 7 | Application | Network services to apps | HTTP, HTTPS, FTP, SMTP, DNS, SSH |
| 6 | Presentation | Data formatting, encryption, compression | SSL/TLS, JPEG, ASCII |
| 5 | Session | Manage communication sessions | NetBIOS, RPC |
| 4 | Transport | Reliable data delivery, ports | TCP, UDP |
| 3 | Network | Routing, IP addressing | IP, ICMP, routers |
| 2 | Data Link | MAC addressing, framing | Ethernet, switches |
| 1 | Physical | Raw bit transmission | Cables, fiber, Wi-Fi |

## Mnemonics

- **Layer 7 → 1**: All People Seem To Need Data Processing
- **Layer 1 → 7**: Please Do Not Throw Sausage Pizza Away

## Devices by layer

| Device | Layer |
|---|---|
| Hub / Repeater | 1 |
| Switch / Bridge | 2 |
| Router | 3 |
| Firewall (traditional) | 3/4 |
| Load Balancer | 4/7 |
| Proxy | 7 |

## Encapsulation

Data moves down the layers, each adding a header:

```
Layer 7: Data
Layer 4: Segment (TCP/UDP header)
Layer 3: Packet (IP header)
Layer 2: Frame (Ethernet header)
Layer 1: Bits
```

## Related Notes

- [[TcpIpModel]]
- [[TcpAndUdp]]
- [[IpAddresses]]
