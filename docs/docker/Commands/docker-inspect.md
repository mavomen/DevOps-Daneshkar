---
id: docker-inspect
aliases: []
tags: []
---

# docker inspect

Return detailed metadata about a Docker object (container, image, volume, network).

## Syntax

```bash
docker inspect [OPTIONS] NAME|ID
```

## Examples

```bash
# Full JSON output for a container
docker inspect <container>

# Get specific field with Go template
docker inspect --format '{{.NetworkSettings.IPAddress}}' <container>

# Get environment variables
docker inspect --format '{{.Config.Env}}' <container>

# Get mount points
docker inspect --format '{{.Mounts}}' <container>
```

## Useful inspect templates

```bash
# Container IP address
docker inspect --format '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container>

# Image size
docker inspect --format '{{.SizeRootFs}}' <image>

# Container state
docker inspect --format '{{.State.Status}}' <container>
```

## Notes

- Output is JSON — pipe to `jq` for filtering: `docker inspect <c> | jq '.[0].NetworkSettings'`
- Works on containers, images, volumes, networks, and nodes.

## Related Notes

- [[Commands/docker-ps|docker ps]]
- [[Commands/docker-images|docker images]]
- [[DockerContainer]]
