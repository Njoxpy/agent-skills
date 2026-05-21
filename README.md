# Agent Skills

![alt text](cover.png)

A curated collection of agent skills focused markdown reference guides that Claude Code (and other AI coding assistants) load on demand to follow consistent, production-grade conventions.

## Table of contents

- [What is a skill](#what-is-a-skill)
- [Repository layout](#repository-layout)
- [Available skills](#available-skills)
- [Skill file format](#skill-file-format)
- [Authoring a new skill](#authoring-a-new-skill)
- [Journal](#journal)
- [Conventions](#conventions)
- [References](#references)

## What is a skill

A skill is a single markdown file that teaches an AI agent how to perform a specific task designing an API, documenting an endpoint, building a UI component using the team's preferred conventions. Skills are:

- **Scoped** one topic per file.
- **Actionable** numbered rules with concrete examples.
- **Loadable** picked up by the agent only when relevant, keeping context lean.

## Repository layout

| Directory              | Purpose                                     |
| ---------------------- | ------------------------------------------- |
| [backend/](backend/)   | Backend skills (API design, services, data) |
| [frontend/](frontend/) | Frontend skills (components, design system) |
| [docs/](docs/)         | Documentation skills (API docs, READMEs)    |

## Available skills

| Skill                                          | Area     | Summary                                               |
| ---------------------------------------------- | -------- | ----------------------------------------------------- |
| [api-design](backend/api-design.md)            | Backend  | REST API naming, versioning, and resource conventions |
| [ui-components](frontend/ui-components.md)     | Frontend | Responsive, accessible UI component patterns          |
| [api-documentation](docs/api-documentation.md) | Docs     | Endpoint documentation standards and examples         |

## Skill file format

Every skill starts with YAML frontmatter and an `# Instructions` section.

```markdown
---
name: skill name
description: One-line summary used by the agent to decide when to load this skill.
---

# Skill Title

## Instructions

1. **Rule one**
   - Detail or example.

2. **Rule two**
   - Detail or example.
```

### Required frontmatter

| Field         | Purpose                                               |
| ------------- | ----------------------------------------------------- |
| `name`        | Short human-readable name (lowercase, spaces allowed) |
| `description` | One sentence the agent reads this to decide relevance |

## Authoring a new skill

1. Pick the right directory (`backend/`, `frontend/`, `docs/`).
2. Create `<skill-name>.md` with the frontmatter shown above.
3. Write rules as numbered, **bold-titled** items, each with a concrete example.
4. Add the skill to the [Available skills](#available-skills) table in this README.
5. Keep the file focused split into a new skill rather than letting one file grow past a few screens.

## Conventions

- **No emojis.** Use "Good" / "Bad" labels in place of check/cross marks.
- **Show, don't tell.** Every rule should have at least one concrete example.
- **Minimal and focused.** No speculative guidance, no half-finished sections.
- **Ask first when unsure** about naming, structure, or scope.
- See [CLAUDE.md](CLAUDE.md) for the full ruleset that applies to this repository.

## References

- [Anthropic Agent Skills overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)
