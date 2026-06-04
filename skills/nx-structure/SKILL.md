---
name: use nx structure
description: Overview of the NX monorepo libs/ folder structure. Read when navigating the project, deciding where to put a new library, or understanding how web/mobile feature libraries are organized internally (routes file, page components, sub-views).
---

Libraries are grouped by feature into folders. See `nx-feature-grouping` for the full picture.

## libs/ folder structure

```
libs/
  feature-payments/
    CLAUDE.md
    shared/
    api/
    data-access/
    node-access/
    web/
    cms/

  feature-notifications/
    CLAUDE.md
    shared/
    api/
    data-access/
```

Do NOT put libraries at root level. Do NOT create separate `libs/web/` or `libs/api/` groupings.

## When to create a new feature folder

- A new business domain is introduced (payments, notifications, documents)
- A new group of related routes appears in web or CMS app
- A new third-party integration is added

## The `web/` layer: Angular feature library

Each `web/` library maps to a lazy-loaded route group:

```
/profile       → feature-profile/web/
/payments      → feature-payments/web/
/admin/pay     → feature-payments/cms/
```

### Internal structure of `web/` or `mobile/`

Angular 17+ — standalone components, no NgModule:

```
src/lib/
  page/                      ← detail/entity page
  page-details/              ← sub-view inside detail page
  page-settings/             ← sub-view inside detail page
  {feature}.component.ts     ← root route component
  {feature}.routes.ts        ← route definitions
```

Routes file:
```typescript
export const PAYMENTS_ROUTES: Routes = [
    { path: '', component: PaymentsComponent },
    { path: ':id', component: PaymentsPageComponent },
];
```

## Dependency rules

```
shared/      ← no external deps
api/         ← imports from shared/ only
data-access/ ← imports from shared/ only
node-access/ ← imports from shared/ only
web/ cms/    ← imports from data-access/ and shared/
```

`web/` and `cms/` NEVER import from `api/` directly.
