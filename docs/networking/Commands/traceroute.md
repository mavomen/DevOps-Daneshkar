---
id: traceroute
aliases: []
tags: []
---

# traceroute

Trace the path packets take to reach a destination, showing each hop along the way.

## Basic usage

```bash
# Trace route to a host
traceroute example.com

# Use ICMP instead of UDP
traceroute -I example.com

# Use TCP (bypasses some firewalls)
traceroute -T example.com

# Don't resolve hostnames
traceroute -n example.com

# Max hops
traceroute -m 30 example.com
```

## Output

```
 1  192.168.1.1   1.234 ms  1.123 ms  1.045 ms
 2  10.0.0.1      5.678 ms  5.543 ms  5.432 ms
 3  72.14.236.81  12.345 ms 12.234 ms 12.123 ms
 ...
```

Each row is a hop (router) between you and the destination.

## Notes

- Some routers don't respond to TTL-expired packets (show `* * *`).
- Use `mtr` for a continuously updating view.
- Firewall may block ICMP — try `-T` for TCP-based traceroute.

## Related Notes

- [[Commands/ping|ping]]
- [[RoutingAndGateways]]
- [[OsiModel]]
