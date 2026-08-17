---
id: Dockerfile
aliases: []
tags: []
---

# Dockerfile

A Dockerfile is a text file with sequential instructions for building a Docker image. Each instruction creates a layer in the image.

## Instructions

| Instruction | Purpose | Example |
|---|---|---|
| `FROM` | Base image | `FROM ubuntu:24.04` |
| `WORKDIR` | Working directory inside container | `WORKDIR /app` |
| `COPY` | Copy files from host into image | `COPY . .` |
| `ADD` | Like COPY but supports archives and URLs | `ADD app.tar.gz /app/` |
| `RUN` | Execute commands during build | `RUN apt update && apt install -y nginx` |
| `ENV` | Set environment variable | `ENV APP_ENV=production` |
| `ARG` | Build-time variable (not in final image) | `ARG VERSION=1.0` |
| `EXPOSE` | Document which port the app uses | `EXPOSE 80` |
| `CMD` | Default command when container starts | `CMD ["nginx", "-g", "daemon off;"]` |
| `ENTRYPOINT` | Main executable (always runs) | `ENTRYPOINT ["dotnet", "MyApp.dll"]` |
| `USER` | Run as specific user | `USER appuser` |
| `VOLUME` | Declare mount point for persistence | `VOLUME ["/var/lib/myapp"]` |
| `HEALTHCHECK` | Define health check | `HEALTHCHECK CMD curl -f http://localhost/ \|\| exit 1` |

## ENTRYPOINT vs CMD

- **ENTRYPOINT** — the main command. Always runs. Arguments can be appended.
- **CMD** — default arguments. Overridden by `docker run` arguments.

```bash
# Dockerfile: ENTRYPOINT ["python", "app.py"]
docker run myapp              # runs: python app.py
docker run myapp debug.py     # runs: python app.py debug.py

# Dockerfile: CMD ["python", "app.py"]
docker run myapp              # runs: python app.py
docker run myapp bash         # runs: bash (CMD replaced entirely)
```

## Example Dockerfile

```dockerfile
FROM nginx:alpine
ARG APP_VERSION=1.0
ENV APP_ENV=production
ENV APP_VERSION=${APP_VERSION}
WORKDIR /usr/share/nginx/html
COPY ./html/ .
RUN echo "Building version ${APP_VERSION}" && echo "Env: ${APP_ENV}"
EXPOSE 80
VOLUME ["/usr/share/nginx/html"]
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD wget --spider -q http://localhost/ || exit 1
CMD ["nginx", "-g", "daemon off;"]
```

## Build

```bash
docker build -t myapp:v1 .
docker build --build-arg VERSION=2.0 -t myapp:v2 .
```

## Related Notes

- [[DockerImage]]
- [[WhatIsDocker]]
- [[Commands/docker-build|docker build]]
- [[DockerfileBestPractices]]
