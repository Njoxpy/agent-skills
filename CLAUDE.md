# CLAUDE.md

Context for Claude Code (and other AI assistants) working in this repository.

## Repository purpose

This repo holds **agent skills** — focused markdown reference guides loaded on demand by AI coding assistants to follow consistent, production-grade conventions.

## Layout

| Directory | Contents |
|-----------|----------|
| [backend/](backend/) | Backend skills (e.g. API design) |
| [frontend/](frontend/) | Frontend skills (e.g. UI components, design system) |
| [docs/](docs/) | Documentation skills (e.g. API documentation) |

See [README.md](README.md) for the full skill index and authoring guide.

## Rules

### Style

- **No emojis** anywhere — code, content, commits, comments. Use words like "Good" / "Bad" instead of check/cross marks.

### Process

- **Ask first when unsure.** Do not guess at naming, structure, or scope.
- **Minimal, focused changes.** No speculative abstractions, no half-finished work.

### Skill files

- Every skill file must start with YAML frontmatter containing `name` and `description`, followed by an `# Instructions` section.

  ```markdown
  ---
  name: skill name
  description: One-line summary used by the agent to decide when to load this skill.
  ---

  # Skill Title

  ## Instructions
  ```

### Frontend

- **Always confirm the design system before building UI.** If the project has no documented design system components, ask the user about **Colors** and **Typography** before writing any frontend code.
