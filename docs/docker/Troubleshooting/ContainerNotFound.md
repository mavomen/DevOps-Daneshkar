---
id: ContainerNotFound
aliases: []
tags: []
---

# Container Not Found

Common errors when a container cannot be found or is in the wrong state.

## "No such container"

```bash
Error: No such container: myapp
```

**Causes:**
- Container was removed (`docker rm`).
- Container name/ID is wrong.
- Container was never created.

**Fix:**

```bash
docker ps -a              # list all containers (including stopped)
docker ps -aq | grep my   # search by partial name
```

## "No such container: not running"

```bash
Error: OCI runtime exec failed: not running
```

**Causes:**
- Container is stopped. `docker exec` only works on running containers.

**Fix:**

```bash
docker start <container>       # restart it
docker exec -it <container> bash
```

## "container is not running"

```bash
Error: Container ... is not running
```

**Fix:**

```bash
docker start <container>
# or check why it stopped
docker logs <container>
docker inspect <container> --format '{{.State.ExitCode}}'
```

## "image not found"

```bash
Error: No such image: myapp:latest
```

**Fix:**

```bash
docker images                  # check local images
docker pull myapp:latest       # pull from registry
```

## Related Notes

- [[DockerContainer]]
- [[Commands/docker-ps|docker ps]]
- [[Commands/docker-run|docker run]]
- [[Commands/docker-logs|docker logs]]
