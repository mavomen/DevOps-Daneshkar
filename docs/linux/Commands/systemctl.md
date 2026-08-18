---
id: systemctl
aliases: []
tags: []
---

# systemctl

Control systemd services and system state.

## Syntax

```bash
systemctl [command] [unit]
```

## Common Usage

```bash
systemctl status nginx
```

```bash
systemctl start nginx
```

```bash
systemctl enable nginx
```

```bash
systemctl list-units --type=service
```

## Tips

- start/stop/restart/enable/disable/status are key commands

## Related Notes

- [[SystemdAndInit]]
