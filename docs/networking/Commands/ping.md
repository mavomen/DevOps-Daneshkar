---
id: ping
aliases: []
tags: []
---

# ping

Test connectivity to a host using ICMP echo requests.

## Basic usage

```bash
# Ping a host
ping example.com

# Ping a specific count
ping -c 4 example.com

# Ping with specific interval
ping -i 0.2 example.com

# Ping specific interface
ping -I eth0 192.168.1.1

# Flood ping (root only, stress test)
sudo ping -f example.com

# Ping with specific packet size
ping -s 1400 example.com
```

## Output fields

| Field | Meaning |
|---|---|
| icmp_seq | Sequence number |
| ttl | Time to live |
| time | Round-trip time (ms) |

## Common uses

```bash
# Test local network
ping 192.168.1.1

# Test DNS resolution
ping google.com

# Test loopback
ping 127.0.0.1

# Continuous ping
ping -c 1000 example.com
```

## Notes

- Uses ICMP (Layer 3), not TCP or UDP.
- Some hosts block ICMP — no response doesn't always mean down.
- Use `traceroute` to see the path packets take.

## Related Notes

- [[Commands/traceroute|traceroute]]
- [[Dns]]
- [[TcpAndUdp]]
