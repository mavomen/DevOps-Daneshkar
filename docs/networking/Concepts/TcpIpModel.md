---
id: TcpIpModel
aliases: []
tags: []
---

# TCP/IP Model

The TCP/IP model is the practical networking model used by the internet. It has 4 layers compared to OSI's 7.

## The 4 layers

| TCP/IP Layer | OSI Equivalent | Protocols |
|---|---|---|
| Application | 7, 6, 5 | HTTP, DNS, FTP, SSH, SMTP |
| Transport | 4 | TCP, UDP |
| Internet | 3 | IP, ICMP, ARP |
| Network Access | 2, 1 | Ethernet, Wi-Fi |

## OSI vs TCP/IP

| Aspect | OSI | TCP/IP |
|---|---|---|
| Layers | 7 | 4 |
| Purpose | Theoretical reference | Practical implementation |
| Developed by | ISO | DARPA/US DoD |
| Usage | Education, troubleshooting | Real-world networking |

## Why it matters

- Most networking documentation refers to TCP/IP layers.
- Troubleshooting tools (tcpdump, Wireshark) work at TCP/IP layer boundaries.
- Cloud networking (VPC, security groups) operates at Internet/Transport layers.

## Related Notes

- [[OsiModel]]
- [[TcpAndUdp]]
- [[IpAddresses]]
