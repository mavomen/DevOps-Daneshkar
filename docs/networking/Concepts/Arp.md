---
id: Arp
aliases: []
tags: []
---

# ARP

Address Resolution Protocol maps IPv4 addresses to MAC (hardware) addresses on a local network.

## How it works

1. Device A wants to send data to `192.168.1.20`
2. Device A broadcasts an ARP request: "Who has 192.168.1.20?"
3. Device B responds: "I do — my MAC is aa:bb:cc:dd:ee:ff"
4. Device A caches the mapping in its ARP table

## View ARP table

```bash
arp -n
# or (modern)
ip neigh show
```

## Manage ARP entries

```bash
# Add a static ARP entry
sudo ip neigh add 192.168.1.20 lladdr aa:bb:cc:dd:ee:ff dev eth0

# Delete an ARP entry
sudo ip neigh del 192.168.1.20 dev eth0

# Flush ARP cache
sudo ip neigh flush all
```

## ARP spoofing

ARP has no authentication — any device can send a fake ARP reply. This is exploited in ARP spoofing attacks to intercept traffic (man-in-the-middle).

**Mitigations:**
- Dynamic ARP Inspection (DAI) on managed switches
- Static ARP entries for critical hosts
- VPN encryption (protects data even if intercepted)

## Related Notes

- [[IpAddresses]]
- [[OsiModel]]
- [[Commands/ip|ip]]
