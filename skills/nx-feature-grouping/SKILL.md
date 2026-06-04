---
name: nx — feature-first library grouping
description: Reference for NX monorepo folder structure. Read this before creating any library or deciding where to put code. Each feature is a folder in libs/ containing layers (shared, api, data-access, web, etc.). Defines naming conventions, dependency direction, and project.json tags.
---

## Core principle

Each feature lives in its own **folder** inside `libs/`. Inside that folder — NX libraries split by layer. The folder name IS the feature scope. No project prefix in library names.

```
libs/
  feature-payments/
    CLAUDE.md                ← product description of this feature
    shared/                  ← NX lib: types, DTOs, endpoint interfaces
    api/                     ← NX lib: NestJS backend
    data-access/             ← NX lib: Angular HTTP client (web app)
    node-access/             ← NX lib: Node.js HTTP client (E2E)
    web/                     ← NX lib: Angular web pages/components
    cms/                     ← NX lib: Angular CMS pages (if needed)
    cms-data-access/         ← NX lib: Angular HTTP client for CMS (if needed)

  feature-notifications/
    CLAUDE.md
    shared/
    api/
    data-access/
```

Not all layers are always needed — create only what the feature requires.

## Naming convention

The NX project name becomes: `feature-{feature-name}-{layer}`

Examples:
```
libs/feature-payments/shared/      → feature-payments-shared
libs/feature-payments/api/         → feature-payments-api
libs/feature-payments/web/         → feature-payments-web
```

## Minimum set for a typical feature

```
libs/
  feature-payments/
    CLAUDE.md
    shared/        ← start here — defines the contract
    api/           ← NestJS: controllers, services, entities
    data-access/   ← Angular: signal-based services, Promise-returning methods
    node-access/   ← Node.js: Promise-based HTTP clients for E2E
```

## CLAUDE.md template for a new feature

```markdown
# Feature: {Feature Name}

## What it does
{1-2 sentences describing the business purpose}

## Domain concepts
- **{ConceptA}** — {brief definition}

## API endpoints
{List main endpoint paths once implemented}

## Who uses it
- Web app: {yes/no — what screens}
- CMS: {yes/no — what admin screens}
- Mobile: {yes/no}

## Notes
{Any important constraints, edge cases, or decisions}
```

## Dependency direction

```
shared        ← no framework deps, pure TypeScript
  ↑   ↑   ↑
 api  data-  node-
      access  access
        ↑
     web / cms
```

## Creation order for a new feature

1. Create folder `libs/feature-{name}/`
2. Create `CLAUDE.md` from template
3. Generate `shared/` — endpoint interface, DTOs, error codes
4. Generate `api/` — controller, service, entity
5. Generate `data-access/` — Angular HTTP service
6. Generate `node-access/` — Node.js HTTP client
7. Generate `web/` and/or `cms/` — UI layers last

## NX project.json tags

```json
{ "tags": ["scope:feature-payments", "type:shared"] }
{ "tags": ["scope:feature-payments", "type:api"] }
{ "tags": ["scope:feature-payments", "type:data-access"] }
{ "tags": ["scope:feature-payments", "type:feature"] }
```

## What NOT to do

- Don't add a project prefix to library names
- Don't create flat `libs/feature-payments-api/` at root level
- Don't create separate `libs/web/`, `libs/api/` groupings
- Don't import from `api/` in Angular code
- Don't skip creating `CLAUDE.md`
