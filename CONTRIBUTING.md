# CONTRIBUTING.md

> Contribution guidelines for the DevOps team repository.

The purpose of these rules is to maintain a clean history, improve collaboration, and make our work easier to understand and review.

---

# Commit Style

All commits should follow this format:

```
type(scope): message
```

Examples:

- feat(docker): add nginx reverse proxy lab
- docs(linux): add permissions guide
- fix(ansible): correct inventory configuration

---

# Commit Types

| Type     | Usage                                             |
| -------- | ------------------------------------------------- |
| feat     | Add a new feature, lab, document, or capability   |
| fix      | Fix an error, bug, or incorrect information       |
| docs     | Documentation changes                             |
| perf     | Performance improvements or optimizations         |
| test     | Add or modify tests                               |
| refactor | Improve existing code without changing behavior   |
| chore    | Maintenance tasks, configuration, tooling changes |

---

# Commit Scope

The scope identifies the affected area.

Examples:

```
linux
networking
docker
nginx
ansible
kubernetes
ci-cd
docs
scripts
repo
```

Example:

- feat(docker): add multi-container application lab
- docs(networking): document DNS troubleshooting

---

# Branch Workflow

The main branches are:

```text
main
 |
 └── develop
      |
      └── feature branches
```

---

# Branch Naming

Branches should follow:

```text
type/description
```

Examples:

- feat/docker-compose-lab
- docs/linux-permissions
- fix/nginx-config
- test/ansible-playbook

---

# Pull Request Rules

## Required

- No direct pushes to `main`.
- No direct merges to `main`.
- No individual commits directly on `develop`.
- All changes must go through Pull Requests.
- Every Pull Request must explain:
  - What changed.
  - Why it changed.
  - How it was tested.

---

# Review Rules

Before merging:

- At least one teammate must review the Pull Request.
- Reviewer should check:
  - Correctness.
  - Documentation quality.
  - Maintainability.
  - Possible improvements.

A review is not approval only.

The goal is knowledge sharing.

---

# Merge Rules

Use merge commits.

Fast-forward merges are avoided.

Preferred:

```bash
git merge --no-ff <branch>
```

Reason:

- Preserve project history.
- Keep feature boundaries visible.
- Make future debugging easier.

---

# Pull Request Template

Every PR should include:

```
## Description

What changed?

## Motivation

Why was this needed?

## Testing

How was this verified?

## Related Issue

#123
```

---

# Contribution Expectations

Contributions can include:

- Code
- Documentation
- Labs
- Scripts
- Research
- Testing
- Reviews
- Diagrams

Engineering contribution is not limited to writing code.

---

# Before Creating a Pull Request

Checklist:

- [ ] Changes are tested.
- [ ] Documentation is updated if needed.
- [ ] Commit messages follow the format.
- [ ] Branch is up to date.
- [ ] No unnecessary files are included.
- [ ] Another teammate can understand the change.

---

# Goal

The repository should represent professional engineering practices:

```
Small Change => Clear Commit => Review => Discussion => Merge => Shared Knowledge
```

One thing I intentionally kept: your `--no-ff` rule. For a tiny team, many people would argue it is unnecessary. They are not wrong. But for a learning repository, it has value because the Git history itself becomes a teaching artifact. You are basically turning your mistakes and decisions into archaeology, which is one of the few useful forms of digging humans have invented.
