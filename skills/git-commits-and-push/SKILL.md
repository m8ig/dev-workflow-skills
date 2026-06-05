---
name: git commits and push workflow
description: "Use when committing or pushing changes in any project. Covers Conventional Commits format, optional Jira ticket suffix enforced by commitlint, branch naming, and PR creation flow."
---

## Commit message format

Commits follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification:

```
<type>(optional scope): <description>
```

Common types: `feat`, `fix`, `refactor`, `chore`, `docs`, `test`, `style`, `perf`.

Examples:
```
feat(auth): add refresh token rotation
fix: correct pagination offset calculation
chore: update dependencies
```

## Jira ticket suffix

If the project has a linked Jira project, append the ticket number at the end of the commit message:

```
feat(auth): add refresh token rotation PRJ-1234
```

Check `commitlint.config.js` in the project root — it specifies the Jira project prefix (e.g. `BAZA`, `SCAL`). If that rule is present, **every commit must end with a valid ticket number**, otherwise commitlint will reject it.

If there is no `commitlint.config.js` or no Jira rule inside it, the ticket suffix is optional.

## Branch workflow

Always create a new branch before making changes. Branch off from `develop` if it exists, otherwise from `master`:

```bash
git checkout develop   # or master
git pull
git checkout -b <type>/short-description
```

Branch naming follows the same type prefix as commits:

```
feat/user-profile-page
fix/ui
refactor/auth-module
```

You can reuse the same branch for multiple related changes and push incrementally. For example, `fix/ui` can accumulate several small frontend fixes.

## Push and PR

After pushing the branch, open a Pull Request. All CI checks and tests must pass before the PR can be merged. Do not merge without green checks.

```bash
git push -u origin <branch-name>
```

Then create the PR via GitHub UI or `gh pr create`.
