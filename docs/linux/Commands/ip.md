---
id: ip
aliases: []
tags: []
---

# ip

Show/manipulate routing, devices, and tunnels.

## Syntax

```bash
ip [object] [command]
```

## Common Usage

```bash
ip addr show
```

```bash
ip route show
```

```bash
ip link show
```

```bash
ip addr add 192.168.1.10/24 dev eth0
```

## Tips

- Replaces ifconfig, route, netstat. Objects: addr, link, route, neigh

## Related Notes

- [[NetworkingBasics]]
