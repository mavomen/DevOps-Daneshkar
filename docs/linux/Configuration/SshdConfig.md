---
id: SshdConfig
aliases: []
tags: []
---

# /etc/ssh/sshd_config — SSH Server Configuration

Controls the SSH daemon behavior. Edit with `sudo systemctl reload sshd`.

## Common Directives

```bash
Port 2222                                 # Non-default port
PermitRootLogin no                        # Disable root login
PasswordAuthentication no                 # Key-only auth
PubkeyAuthentication yes                  # Enable key auth
MaxAuthTries 3                            # Limit attempts
AllowUsers alice bob                      # Whitelist users
ClientAliveInterval 300                   # Timeout (seconds)
ClientAliveCountMax 2                     # Max missed keepalives
```

## Security Hardening

```bash
# /etc/ssh/sshd_config hardening
Port 2222
PermitRootLogin no
PasswordAuthentication no
PermitEmptyPasswords no
X11Forwarding no
AllowAgentForwarding no
MaxAuthTries 3
LoginGraceTime 30
```

## Reload & Test

```bash
sudo sshd -t                              # Test config syntax
sudo systemctl reload sshd                # Apply changes
sudo ss -tlp | grep sshd                  # Verify port
```

## Related Notes

- [[SecurityHardening]] — System hardening
- [[NetworkingBasics]] — Network fundamentals
- [[SystemStatus]] — System investigation
