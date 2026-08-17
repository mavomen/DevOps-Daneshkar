---
id: docker-diff
aliases: []
tags: []
---

# docker diff

Show filesystem changes made inside a container since it was created.

## Syntax

```bash
docker diff CONTAINER
```

## Output format

```
A /app/config.yml        # Added
C /var/log/app.log       # Changed
D /tmp/cache             # Deleted
```

| Code | Meaning |
|---|---|
| `A` | Added |
| `C` | Changed |
| `D` | Deleted |

## Examples

```bash
# See all changes
docker diff mycontainer

# Combined with commit workflow
docker diff mycontainer
docker commit mycontainer myapp:v2
```

## When to use

- Debugging: see what changed inside a container before committing.
- Verification: confirm that a setup script modified the expected files.
- Pre-commit check: review changes before creating an image with `docker commit`.

## Notes

- Works on both running and stopped containers.
- Compares current filesystem to the original image layer.
- Only shows changes, not the full filesystem.

## Related Notes

- [[Commands/docker-commit|docker commit]]
- [[Commands/docker-exec|docker exec]]
- [[DockerContainer]]
