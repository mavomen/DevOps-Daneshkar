---
id: RepositoryStructure
aliases: []
tags: []
---

# Repository Structure

A predictable repository structure improves onboarding, automation, and maintainability.

## Goals

- make “where things live” obvious
- reduce accidental coupling
- support tooling (CI, linting, releases)

Related:

- [[CiCdIntegration]]
- [[GitIgnorePatterns]]
- [[GitAttributes]]

## Common top-level layout (generic)

Example:

- `README.md`
- `LICENSE`
- `docs/`
- `src/`
- `tests/`
- `scripts/`
- `.github/` (or `.gitlab/`)
- `.editorconfig` (optional)
- `.gitignore`
- `.gitattributes`

## Keep configuration discoverable

- CI config near root (`.github/workflows`, `.gitlab-ci.yml`)
- tool configs at root if the tool expects it (`package.json`, `pyproject.toml`, etc.)
- scripts in `scripts/` with clear names

## Documentation hygiene

- `README.md` should cover:
  - what it is
  - how to run
  - how to test
  - how to contribute
- larger docs in `docs/`
- add `CONTRIBUTING.md` if you expect external contributions

## “Generated” and “local” files

- generated artifacts should typically NOT be committed
  - add to `.gitignore` (see [[GitIgnorePatterns]])
- if you must commit generated outputs, document why and how they’re produced

## Versioning strategy

- tag releases (see [[git-tag]])
- keep version source-of-truth clear (single file if possible)

## Related notes

- [[BestPractices/RepositoryManagement/LargeRepositoryHandling|Large Repository Handling]]
- [[BestPractices/RepositoryManagement/MonorepoVsMultirepo|Monorepo vs Multirepo]]
