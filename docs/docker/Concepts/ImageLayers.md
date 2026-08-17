---
id: ImageLayers
aliases: []
tags: []
---

# Image Layers

Every Docker image is composed of read-only layers. Each layer represents a filesystem change made by a Dockerfile instruction.

## How layers work

```dockerfile
FROM ubuntu:24.04          # Layer 0: base OS
RUN apt update            # Layer 1: package lists
RUN apt install -y curl   # Layer 2: curl binary
COPY . /app               # Layer 3: application files
```

Each layer only stores the diff from the previous layer.

## Layer properties

| Property | Description |
|---|---|
| **Immutable** | Once created, never changed |
| **Content-addressable** | Identified by SHA256 hash of content |
| **Shared** | Multiple images can share common layers |
| **Cached** | Docker reuses layers unless changes are detected |

## Copy-on-Write

When a container starts, Docker adds a thin writable layer on top of the image layers. All changes (new files, modified files) go into this writable layer.

```
Container writable layer (thin, temporary)
Image layer N   (read-only)
Image layer N-1 (read-only)
...
Image layer 0   (read-only)
```

## Layer cache

Docker caches layers during build. If a layer's instruction and inputs haven't changed, Docker reuses the cached version.

```bash
# See layer sizes
docker history myimage:v1

# Detailed layer info
docker inspect myimage:v1
```

## Layer cache invalidation

Layers are rebuilt from the point of change onward:

```dockerfile
# If package.json changes, these layers rebuild
COPY package*.json ./
RUN npm ci

# Even though this hasn't changed, it rebuilds too
COPY . .
```

## Dangling vs intermediate images

| Type | What | How to clean |
|---|---|---|
| Dangling | Untagged images from rebuilds | `docker image prune` |
| Intermediate | Intermediate build layers | Prune after build completes |

## Disk usage

```bash
# Image size breakdown
docker system df -v
```

## Related Notes

- [[DockerImage]]
- [[Dockerfile]]
- [[Commands/docker-history|docker history]]
- [[Commands/docker-images|docker images]]
