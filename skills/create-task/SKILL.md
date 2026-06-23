---
name: create a task
description: Use when creating a task or bug report in any issue tracker. Covers description structure, screenshot requirements, and environment defaults.
---

## Determining the issue-tracker project

When the tracker is Jira, determine the project key from the repo's `commitlint.config.js` — look at `parserPreset.parserOpts.issuePrefixes`. The prefix is the Jira project key. Example: `issuePrefixes: ['BAZA-']` → project key `BAZA`.

## Rules for creating a task

- **No file paths or technical internals in the description.** Don't mention file names, component names, function names, or implementation details — these belong in code comments or PR descriptions, not in the ticket.
- **Write for a non-technical reader.** The description should clearly explain what the user sees, what they expect to happen, and what actually happens. Avoid jargon, framework names, and code terms.
- **Attach a screenshot when possible.** Navigate to the production or test site, reproduce the issue, and include a screenshot to make the problem immediately visible.
- **Default environment is test** unless explicitly stated otherwise. If the issue is reported on production, note that clearly.
- **Bug description structure:** What the user did → what they expected → what happened instead.
- **Task description structure:** Context (why this is needed) → what needs to be done from the user's perspective → acceptance criteria (how to verify it's done).
