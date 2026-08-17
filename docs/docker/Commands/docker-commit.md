---
id: docker-commit
aliases: []
tags: []
---

# docker commit

Create a new image from the current state of a container.

## Syntax

```bash
docker commit [OPTIONS] CONTAINER IMAGE[:TAG]
```

## Workflow

```bash
# 1. Run a container
docker run -dit --name mybuild ubuntu

# 2. Make changes inside it
docker exec -it mybuild bash
# ... install packages, modify files ...

# 3. Commit the container state as a new image
docker commit mybuild myapp:v1

# 4. Verify
docker images
```

## Options

| Option | Purpose |
|---|---|
| `-m` | Commit message |
| `-a` | Author name |

```bash
docker commit -m "Added nginx config" -a "dev" mybuild myapp:v1
```

## When to use

- Quick debugging: create a container, poke around, commit the state.
- Prototyping: test changes before writing them into a Dockerfile.
- **Not recommended** for production images — prefer Dockerfiles for reproducibility.

## Related Notes

- [[DockerImage]]
- [[Dockerfile]]
- [[Commands/docker-run|docker run]]
- [[Commands/docker-images|docker images]]
