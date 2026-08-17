---
id: MultiStageBuild
aliases: []
tags: []
---

# Multi-Stage Build

Multi-stage builds let you use multiple `FROM` statements in a single Dockerfile. Each stage builds independently, and only the final stage's files end up in the final image.

## Why use it

- Build code in a heavy image (with compilers, SDKs).
- Copy only the compiled output to a slim runtime image.
- Dramatically smaller final image size.

## Example: Go application

```dockerfile
# Stage 1: Build
FROM golang:1.22 AS builder
WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 go build -o server .

# Stage 2: Run
FROM alpine:3.19
WORKDIR /app
COPY --from=builder /app/server .
EXPOSE 8080
CMD ["./server"]
```

Result: final image contains only `alpine` + the Go binary. No Go compiler, no source code.

## Example: Node.js application

```dockerfile
# Stage 1: Install dependencies and build
FROM node:20 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Stage 2: Serve with nginx
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
```

## Copy from a specific stage

```bash
COPY --from=builder /app/dist ./dist
COPY --from=0 /app/config.yml ./config.yml
```

## Tips

- Name stages with `AS` for readability.
- Use `--target` to build up to a specific stage: `docker build --target builder .`
- Combines well with `.dockerignore` to keep build context small.

## Related Notes

- [[Dockerfile]]
- [[DockerfileBestPractices]]
- [[Commands/docker-build|docker build]]
