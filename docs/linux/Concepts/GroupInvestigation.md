---
id: GroupInvestigation
aliases: []
tags: []
---

# Group Investigation

Investigating group membership for security incident response.

## /etc/group

The system group database. Defines all groups and their members.

```bash
cat /etc/group
```

### Format

```
group_name:password:GID:member_list
```

### User's Groups (mava)

| Group | GID | Significance |
|-------|-----|--------------|
| `wheel` | 998 | Admin group — can run `sudo` |
| `docker` | 964 | Can run Docker without `sudo` |
| `mava` | 1000 | Primary group |

> [!WARNING]
> Docker group membership is effectively root access (can mount host filesystem into containers).

### Hardware Access Groups

| Group | Purpose |
|-------|---------|
| `audio` | Sound cards |
| `video` | GPU, framebuffer |
| `render` | GPU rendering (Vulkan/Mesa) |
| `kvm` | KVM virtualization |
| `input` | Keyboard, mouse |
| `storage` | External drives |
| `disk` | Raw disk access (dangerous) |

### System/Service Groups

| Group | Purpose |
|-------|---------|
| `systemd-journal` | Read journal logs without sudo |
| `systemd-network` | Network management |
| `systemd-resolve` | DNS |
| `polkitd` | Authorization framework |
| `docker` | Container runtime |

## Quick Verification

```bash
groups mava                                # All groups for user
id mava                                    # UID, GID, supplementary groups
```

## Related Notes

- [[UserAccountInvestigation]] — User account details
- [[SudoConfiguration]] — Sudo rules
- [[03-SecurityMOC]] — Linux Security MOC
