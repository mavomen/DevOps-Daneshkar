---
id: CiCdIntegration
aliases: []
tags: []
---

# CI/CD Integration

How Git practices connect to CI/CD pipelines: triggers, fetch depth, tags/releases, and safe defaults.

## Suggested Aliases (optional)

- `CI CD Integration`
- `CI/CD Integration`

## What CI/CD Usually Does

On each push or PR/MR:

- checkout repository
- install dependencies
- run lint/tests
- build artifacts
- (optionally) deploy

## Key Git Concerns for CI

### Shallow clones (fetch depth)

Many CI systems default to shallow clone for speed.
If your pipeline needs tags or history (release notes, versioning), ensure full history or tags are fetched.

### Tags for releases

Tags often trigger release jobs:

- create annotated tags via [[git-tag]]
- push tags via [[git-push]]

### Branch protection + required checks

Teams often require:

- CI checks passing before merge
- review approvals
- no direct pushes to `main`

See: [[Workflows/CodeReviewWorkflow]]

## Example: GitHub Actions (minimal)

Create `.github/workflows/ci.yml`:

```yaml
name: CI

on:
  push:
    branches: ["main"]
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0 # full history if you need tags/versioning

      - name: Install
        run: npm ci

      - name: Test
        run: npm test
```

## Example: GitLab CI (minimal)

Create `.gitlab-ci.yml`:

```yaml
stages: [test]

test:
  image: node:20
  stage: test
  script:
    - npm ci
    - npm test
```

## Hook + CI Pairing (Good Practice)

- local hooks (see [[GitHooks]]) catch issues early
- CI enforces the same checks for everyone

## Related Notes

- [[GitHooks]]
- [[Workflows/CodeReviewWorkflow]]
- [[git-fetch]]
- [[git-tag]]
- [[git-push]]
