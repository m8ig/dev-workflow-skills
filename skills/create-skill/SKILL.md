---
name: create a skill
description: "Use when creating a new skill for the LLM skills system. Covers file structure, categories (be/fe/org), registration in Claude and Codex, dev-workflow-skills repo, and YAML frontmatter conventions."
---

A skill is a reusable instruction set loaded into the AI assistant on demand. Skills live in the Knowledge base and are registered separately in Claude and Codex.

## Folder structure

Skill content files are stored in `/Users/m8ig/Knowledge/LLM skills/` under one of three categories:

- `be/` — backend skills (NestJS, API, Redis, CQRS, etc.)
- `fe/` — frontend skills (Angular, NGXS, components, styles, etc.)
- `org/` — organizational and process skills (repo setup, Jira, skill creation, etc.)

Put the new skill in the category that matches its scope.

## Files to create

Creating a skill requires 3 files:

**1. Content file** — the actual instructions, plain Markdown, no frontmatter:
```
/Users/m8ig/Knowledge/LLM skills/<category>/<Skill name>.md
```

**2. Claude registration** — frontmatter + `@reference` to the content file:
```
/Users/m8ig/.claude/skills/<skill name>/SKILL.md
```

**3. Codex registration** — same format as Claude:
```
/Users/m8ig/.codex/skills/<skill name>/SKILL.md
```

The registration files look like this:
```markdown
---
name: skill name in lowercase
description: "One sentence: when to use this skill."
---

@/Users/m8ig/Knowledge/LLM skills/<category>/<Skill name>.md
```

## dev-workflow-skills repo

Skills are also tracked in the git repo `/Users/m8ig/Git/dev-workflow-skills/`. Each skill gets its own folder with a slug name:
```
skills/<skill-slug>/SKILL.md
```

This file contains the frontmatter + full content inline (not a `@reference`). The slug uses kebab-case, e.g. `create-a-skill`.

After adding, commit and push the changes.

## YAML gotcha

The `description` field in frontmatter **must be quoted with double quotes** if it contains `: ` (colon followed by a space). Without quotes the YAML parser throws:

```
Error in user YAML: mapping values are not allowed in this context
```

Always quote the description to be safe:
```yaml
description: "Use when creating a new skill. Covers file structure, registration, and YAML conventions."
```

## Description format

The `description` field should explain **when** to use the skill, not what it is. Start with "Use when…" so the assistant knows when to load it automatically.
