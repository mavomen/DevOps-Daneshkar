---
id: IpAddresses
aliases: []
tags: []
---

# IP Addresses

An IP (Internet Protocol) address is a unique identifier assigned to a device on a network. It identifies the device and locates it for data delivery.

## IPv4

- 32-bit address
- Written as four decimal numbers separated by dots
- Range: 0.0.0.0 to 255.255.255.255
- Example: `192.168.1.25`

## IPv6

- 128-bit address
- Written in hexadecimal, eight groups separated by colons
- ~3.4 × 10³⁸ addresses
- Example: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- Leading zeros can be omitted: `2001:db8:85a3::8a2e:370:7334`

## Address types

| Type | Description | Example |
|---|---|---|
| Unicast | One-to-one | `192.168.1.10` → `192.168.1.20` |
| Broadcast | One-to-all on LAN (IPv4 only) | `192.168.1.255` |
| Multicast | One-to-group | `224.0.0.1` (all hosts) |
| Anycast | One-to-nearest | Used in DNS, CDN |

## Private vs public IPs

| Private ranges | Use |
|---|---|
| `10.0.0.0/8` | Large networks |
| `172.16.0.0/12` | Medium networks |
| `192.168.0.0/16` | Home/small office |

Private IPs cannot be routed on the internet. Use NAT to translate.

## Loopback

- IPv4: `127.0.0.1`
- IPv6: `::1`
- Used for testing the local TCP/IP stack

## Related Notes

- [[Subnetting]]
- [[NatAndPAT]]
- [[TcpAndUdp]]
