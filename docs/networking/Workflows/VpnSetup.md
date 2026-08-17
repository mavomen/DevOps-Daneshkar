---
id: VpnSetup
aliases: []
tags: []
---

# VPN Setup

Configure VPN connections for secure remote access.

## WireGuard Setup

```bash
# Install WireGuard
sudo apt install wireguard

# Generate keys
wg genkey | tee privatekey | wg pubkey > publickey

# Configure /etc/wireguard/wg0.conf
[Interface]
PrivateKey = <private_key>
Address = 10.0.0.2/24
DNS = 8.8.8.8

[Peer]
PublicKey = <server_public_key>
Endpoint = vpn.example.com:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 25

# Start/stop
sudo wg-quick up wg0
sudo wg-quick down wg0
sudo systemctl enable wg-quick@wg0
```

## OpenVPN Setup

```bash
# Install OpenVPN
sudo apt install openvpn

# Connect to VPN
sudo openvpn --config client.ovpn

# Verify connection
curl ifconfig.me
```

## Related Notes

- [[NetworkSecurity]] - Security hardening
- [[RoutingTables]] - Routing configuration
- [[DnsResolution]] - DNS through VPN
