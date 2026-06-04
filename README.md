# Dev Workflow Skills

A collection of 9 skills for development workflow and project organization. Covers NX monorepo structure, code formatting, pre-commit hooks, task management, and shared library patterns.

Compatible with **Claude Code** and **OpenAI Codex**.

## Skills

| Skill | Description |
|---|---|
| `add-formatter` | Use when setting up code formatting for a new project. Covers Prettier installation and the standard .prettierrc config used across projects. |
| `add-pre-commit` | Use when setting up pre-commit hooks for a project. Covers Husky + Commitlint + lint-staged configuration to enforce code quality and commit message format before every commit. |
| `create-new-repo` | Use when initializing a new git repository. Covers default branch naming, .gitignore, and initial project setup conventions. |
| `create-shared-library` | Use when creating the contract layer for a new feature — the starting point before API or Angular code. Contains DTOs, endpoint interfaces, enums, and error codes. Pure TypeScript only. |
| `create-task` | Use when creating a task or bug report in any issue tracker. Covers description structure, screenshot requirements, and environment defaults. |
| `nx-feature-grouping` | Reference for NX monorepo folder structure. Read this before creating any library or deciding where to put code. Each feature is a folder in libs/ containing layers. |
| `nx-library-types` | Reference for what goes into each NX library layer (shared, api, data-access, node-access, web, cms). |
| `nx-structure` | Overview of the NX monorepo libs/ folder structure and how web/mobile feature libraries are organized internally. |
| `set-priorities` | Read this first before any development task. Defines the priority hierarchy: skills → AGENTS.md → user instructions. |

## Installation

### Claude Code

```
claude plugin add m8ig/dev-workflow-skills
```

### OpenAI Codex

```bash
git clone https://github.com/m8ig/dev-workflow-skills /tmp/dev-workflow-skills
cp -r /tmp/dev-workflow-skills/skills/* ~/.codex/skills/
```

## Usage

### Claude Code

```
/nx-feature-grouping
/create-shared-library
/set-priorities
```

### OpenAI Codex

```
$nx-feature-grouping
$create-shared-library
```

Skills also activate automatically when your task matches the skill description.
