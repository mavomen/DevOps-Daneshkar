# Proposed Team Structure

> Team structure, responsibilities, workflow, and collaboration rules.

## Team Structure

| Name     | Role                                | Responsibilities                                                                                                                                                                                                                                                                                  |
| -------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mava     | Technical Lead / Platform Architect | - Define repository architecture and engineering standards<br>- Review pull requests<br>- Guide technical decisions<br>- Handle complex debugging<br>- Mentor teammates<br>- Introduce advanced topics (CI/CD, Kubernetes, architecture, automation)<br>- Ensure projects are production-oriented |
| Shaqayeq | Infrastructure Engineer             | - Own Linux, Nginx, Docker topics<br>- Build and maintain infrastructure labs<br>- Document infrastructure knowledge<br>- Review beginner contributions<br>- Progress toward Ansible, networking, Kubernetes<br>- Lead practical deployment tasks                                                 |
| Hengameh | Systems Apprentice                  | - Build Linux fundamentals<br>- Learn Git workflow<br>- Practice command line skills<br>- Document learning progress<br>- Complete beginner labs<br>- Gradually take ownership of foundational topics                                                                                             |

---

## Team Priorities

### 1. Understand Class Material

The bootcamp curriculum is the foundation.

The team should:

- Follow the class topics.
- Clarify difficult concepts together.
- Extend topics with practical examples.
- Avoid skipping fundamentals for advanced technologies.

### 2. Document Everything

Learning should become reusable knowledge.

Documentation should include:

- Concepts
- Commands
- Examples
- Troubleshooting
- Lessons learned
- Common mistakes

A finished document should help another person understand the topic without needing the original author.

---

## Decision Making

### Technical Decisions

Technical decisions should follow ownership.

The person responsible for a topic leads the discussion and proposes solutions.

Examples:

- Docker decisions → Infrastructure Engineer
- Repository architecture → Technical Lead
- Beginner learning structure → Apprentice with team support

Important decisions should be documented.

Example:

```markdown
Decision:
Use Docker Compose instead of Kubernetes for the first deployment lab.

Reason:
The project goal is understanding containers and networking before orchestration.
```

### Team Decisions

General team decisions use majority voting.

Examples:

- Meeting schedule
- Project selection
- Repository organization
- Workflow changes

---

## Contribution Workflow

All meaningful work should follow:

```
Task => Issue => Branch => Implementation => Pull Request => Review => Merge
```

---

## TaskBoard

**GitHub Projects**

Reasons:

- Integrated with the repository.
- Keeps tasks close to the code and documentation.
- Creates visible engineering history.
- Useful for future portfolio review.

### Board Structure

```
Backlog => Ready => In Progress => Review => Done
```

---

## Current Focus

### Bootcamp Period

Priority order:

1. Follow bootcamp material.
2. Strengthen fundamentals.
3. Build practical labs.
4. Create portfolio projects.
5. Prepare for DevOps job applications.
