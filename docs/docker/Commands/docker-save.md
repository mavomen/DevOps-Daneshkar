---
id: docker-save
aliases: []
tags: []
---

# docker save / docker export

Export images and containers for offline transfer or backup.

## docker save — image to tar

Exports an image (with all layers) to a tar file.

```bash
# Save an image
docker save -o myapp.tar myapp:v1

# Save multiple images
docker save -o images.tar myapp:v1 nginx:alpine
```

## docker load — tar to image

Import a saved image back.

```bash
docker load -i myapp.tar
```

## docker export — container filesystem to tar

Exports a container's filesystem as a tar archive (flattened, no layers).

```bash
docker export mycontainer > container.tar
```

## docker import — tar to image

Create an image from a tar archive.

```bash
docker import container.tar myimage:v1
```

## save/export comparison

| | `docker save` | `docker export` |
|---|---|---|
| Input | Image | Container |
| Output | Tar with layers | Flattened tar |
| Preserves layers | Yes | No |
| Use case | Backup/transfer images | Backup container filesystem |

## Related Notes

- [[DockerImage]]
- [[DockerContainer]]
- [[Commands/docker-images|docker images]]
