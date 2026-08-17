---
id: firewalld
aliases: []
tags: []
---

# firewalld and UFW

Dynamic firewall management tools that simplify `iptables` configuration.

## firewalld (CentOS/RHEL)

```bash
# Check status
sudo firewall-cmd --state

# List open ports
sudo firewall-cmd --list-ports

# Open a port
sudo firewall-cmd --add-port=80/tcp --permanent

# Close a port
sudo firewall-cmd --remove-port=80/tcp --permanent

# Open a service
sudo firewall-cmd --add-service=http --permanent

# Reload after permanent changes
sudo firewall-cmd --reload

# List all services
sudo firewall-cmd --get-services
```

## UFW (Ubuntu)

```bash
# Enable
sudo ufw enable

# Check status
sudo ufw status verbose

# Allow by port
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# Allow by application
sudo ufw allow "OpenSSH"
sudo ufw allow "Nginx Full"

# Deny a specific IP
sudo ufw deny from 10.0.0.50

# Delete a rule
sudo ufw delete allow 80/tcp

# Reset to defaults
sudo ufw reset
```

## firewalld vs UFW vs iptables

| Tool | Complexity | Best for |
|---|---|---|
| iptables | High | Full control, scripting |
| firewalld | Medium | RHEL/CentOS, dynamic rules |
| UFW | Low | Ubuntu, quick setup |

## Related Notes

- [[Commands/iptables|iptables]]
- [[Firewall]]
- [[Commands/netstat|netstat]]
