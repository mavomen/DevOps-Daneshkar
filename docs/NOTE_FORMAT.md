# Note Format (Dominant Standard)

> One format for every note in this repository. Source of truth for what a note looks like and how it is named. The canonical template is `templates/note-template.md`.

## Anatomy

Every note follows this exact order:

```markdown
---
id: <FileName>
aliases: []
tags: []
---

# <Title>

<One to two sentences: what this note covers and when to reach for it.>

## <Section Topic>
...

## Related Notes
- [[<FileName>]]
```

## Rules

### Frontmatter

- Every note starts with the Obsidian-style block: `id`, `aliases: []`, `tags: []`.
- `id` must match the file name (without extension).
- Keep `aliases` and `tags` as empty arrays unless they are actually used.

### Title and summary

- `# H1` title matches the file name / note name.
- Exactly one short summary line below the title: what this covers and when to reach for it. This line is not a heading.

### Body

- Use focused `##` sections. Each section covers one idea.
- Use `###` sparingly; never nest deeper than `###`.
- Prefer copy-paste-ready ` ```bash ` blocks and small markdown tables over long prose.
- Write in English, in the imperative, with concrete examples (inputs/outputs).

### Closing section

- Every note ends with `## Related Notes` — a bullet list of `[[wiki-links]]`.
- Only link notes that exist. Do not invent links to future notes.
- `## Related Notes` is the one and only "related" section. Do not use `Related Commands`, `Related Concepts`, or `Quick Reference` as headings.

### Wiki-link style

- Use the short unique name: `[[NoteName]]`.
- Use the full relative path with a display alias only when the basename is not unique across the repo:

```markdown
[[Concepts/ConflictResolution|Conflict Resolution]]
```

## File naming

| Note type                 | Pattern                       | Example                              |
| ------------------------- | ----------------------------- | ------------------------------------ |
| Concepts / Workflows / BestPractices / Troubleshooting | `PascalCase.md` | `MergeConflicts.md`, `FeatureBranchWorkflow.md` |
| Command notes             | `<tool>-<name>.md`            | `git-commit.md`, `docker-compose.md` |
| Index / MOC notes         | `NN-SubjectMOC.md`            | `02-DailyWorkflowMOC.md`             |

Guidelines:

- One note per topic. No duplicate file names anywhere in `docs/`.
- Use `PascalCase` consistently (`TeamPractices`, not `TeamPracties`).
- Keep MOC numbering lowercase-later (`02-DailyWorkflowMOC`, not `02-DailyWOrkflowMOC`).

## Anti-patterns (do not do these)

- 300+ line encyclopedia dumps. Split into focused notes and link them.
- Inconsistent related-section names. Always `## Related Notes`.
- Mermaid diagrams by default. Only add them when a diagram is genuinely clearer than a list.
- Deep heading nesting (`####`+).
- Mixed link styles within one note.
- Dead frontmatter keys or `id` values that do not match the file name.
- Leftover `TODO` / `FIXME` / unfinished blocks in committed notes.

## Directory pattern

Each topic directory under `docs/` mirrors the git vault structure:

```text
docs/<topic>/
├── NN-SubjectMOC.md        # optional index notes (00-Subject.md → NN-MOCs)
├── Concepts/
├── Commands/
├── Workflows/
├── Configuration/
├── BestPractices/
├── Troubleshooting/
├── QuickReference/
├── ScenariosAndExercises/
└── Resources/
```

Index/MOC notes are plain lists of `[[wiki-links]]` organized by learning path. They follow the same anatomy: frontmatter, `# H1` ending in `(MOC)`, summary, then link sections.
