---
name: use different types of nx libraries
description: Reference for what goes into each NX library layer (shared, api, data-access, node-access, web, cms). Read this when deciding which library type to create or which layer a piece of code belongs to.
---

Each feature folder contains multiple NX libraries — one per layer.

**For folder structure and naming:** see `nx-feature-grouping`.

---

## `shared/` — Contract layer (no framework)

Pure TypeScript. Zero Angular, zero NestJS. Single source of truth.

**NX project name:** `feature-{name}-shared`

**Contains:** endpoint interfaces, request/response DTOs, error code enums, domain models, CQRS commands/events, i18n strings

**Depends on:** nothing framework-specific

---

## `api/` — NestJS backend

**NX project name:** `feature-{name}-api`

**Contains:** NestJS controllers, services, TypeORM entities, repositories, mappers, exceptions, CQRS handlers

**Depends on:** `shared/`

Controller implements the endpoint interface from `shared/`. Error codes always imported from `shared/`.

---

## `data-access/` — Angular HTTP client

Observable-based Angular services for the web app.

**NX project name:** `feature-{name}-data-access`

**Contains:** `@Injectable` Angular services implementing endpoint interfaces

**Depends on:** `shared/`

---

## `node-access/` — Node.js HTTP client

Promise-based plain classes for E2E tests and scripts.

**NX project name:** `feature-{name}-node-access`

**Contains:** plain TypeScript classes implementing endpoint interfaces

**Depends on:** `shared/`

---

## `web/` — Angular web feature

**NX project name:** `feature-{name}-web`

**Contains:** lazy-loaded standalone page components, route config

**Depends on:** `data-access/`, `shared/`

Angular 17+ — no NgModule, routes defined inline:

```ts
export const FEATURE_ROUTES: Routes = [
    { path: '', component: FeatureComponent },
    { path: ':id', component: FeaturePageComponent },
];
```

Internal structure:
```
page/                        ← detail page
page-settings/               ← child sub-view
{feature}.component.ts       ← root route component
{feature}.routes.ts
```

---

## `mobile/` — Angular mobile (Capacitor)

Same structure as `web/` but for mobile.

**NX project name:** `feature-{name}-mobile`

**Contains:** standalone components with Tailwind CSS (iOS tokens)

---

## `cms/` — Angular CMS feature

Same structure as `web/` but for the admin CMS.

**NX project name:** `feature-{name}-cms`

---

## `cms-data-access/` — Angular HTTP client for CMS

Same as `data-access/` but uses `BazaCmsDataAccessService`.

Only needed when CMS calls different endpoints than the web app.

---

## Dependency summary

```
shared/
  ↑            ↑            ↑
api/       data-access/  node-access/
                ↑
           web/ / cms/
```

Never import sideways between features. Cross-feature dependencies go through `shared/` only.
