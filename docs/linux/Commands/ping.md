---
id: ping
aliases: []
tags: []
---

# ping

Send ICMP echo requests to test connectivity.

## Syntax

```bash
ping [options] host
```

## Common Usage

```bash
ping -c 4 8.8.8.8
```

```bash
ping -c 100 -i 0.2 target
```

```bash
ping -s 1472 -M do target
```

## Tips

- -c for count, -i for interval, -s for packet size, -M do tests MTU

## Related Notes

- [[NetworkingBasics]]
