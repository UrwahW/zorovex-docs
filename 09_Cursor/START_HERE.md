# Start Here

This folder contains Cursor-ready engineering tasks for Zorovex.

Every task is a specification. Read it. Implement it. Stop when done.

Do not skip ahead. Do not combine tasks. Do not redesign.

---

# Before You Write Code

1. Read [Cursor_Rules.md](Cursor_Rules.md) — mandatory for every task.
2. Read the sprint overview in [08_Sprints/](../08_Sprints/).
3. Open the task file for the work you are doing.
4. Read every document listed under **Read First** in that task.

Documentation wins over assumptions.

---

# How to Run a Task in Cursor

1. Open the task file (e.g. `@09_Cursor/Sprint_01/AUTH-001.md`).
2. Tell the agent:

   ```
   Read @09_Cursor/START_HERE.md and @09_Cursor/Cursor_Rules.md.
   Implement the task in @09_Cursor/Sprint_01/AUTH-001.md exactly.
   Stop when Acceptance Criteria are met. Do not start the next task.
   ```

3. Verify every item in **Acceptance Criteria** before moving on.
4. Update the docs listed in the task when implementation changes behavior.

---

# Sprint 01 — Task Order

Complete tasks in this order:

| Order | Task | Title |
|-------|------|-------|
| 1 | [AUTH-001](Sprint_01/AUTH-001.md) | Bootstrap Zorovex Backend |
| 2 | [AUTH-002](Sprint_01/AUTH-002.md) | Login and JWT Issuance |
| 3 | [AUTH-003](Sprint_01/AUTH-003.md) | JWT Auth Middleware |
| 4 | [ORG-001](Sprint_01/ORG-001.md) | Organization Data Model |
| 5 | [ORG-002](Sprint_01/ORG-002.md) | Create Organization on Registration |
| 6 | [AUTH-004](Sprint_01/AUTH-004.md) | Roles and RBAC Seed |
| 7 | [AUTH-005](Sprint_01/AUTH-005.md) | Current User Endpoint |
| 8 | [ORG-003](Sprint_01/ORG-003.md) | Organization Settings API |
| 9 | [UI-001](Sprint_01/UI-001.md) | Login and Register Pages |
| 10 | [UI-002](Sprint_01/UI-002.md) | Dashboard Shell Layout |
| 11 | [BUS-001](Sprint_01/BUS-001.md) | Business Setup Wizard |

Sprint goal: [Sprint_01.md](../08_Sprints/Sprint_01.md)

---

# Folder Layout

```
09_Cursor/
├── START_HERE.md       ← you are here
├── Cursor_Rules.md     ← engineering rules (locked)
├── Sprint_01/          ← active tasks
├── Sprint_02/          ← upcoming
├── Sprint_03/
└── Sprint_04/
```

---

# Task Naming

| Prefix | Area |
|--------|------|
| AUTH | Authentication and authorization |
| ORG | Organizations and multi-tenancy |
| UI | Frontend screens and layout |
| BUS | Business setup and onboarding |

Format: `{PREFIX}-{NNN}.md` (e.g. `AUTH-001.md`)

---

# Definition of Done

A task is complete when:

- Every **Acceptance Criteria** item passes
- Tests run and pass
- Linting passes (Rubocop / ESLint as applicable)
- Referenced documentation is updated
- No scope from **Out of Scope** was added
- You stopped — did not begin the next task

---

# Where Code Lives

| Repo / folder | Purpose |
|---------------|---------|
| `zorovex-docs/` | Specifications, architecture, tasks (this repo) |
| `backend/` | Rails 8 API (created in AUTH-001) |
| `frontend/` | React + TypeScript app |

Specs live here. Code lives in application repos.

---

# First Task

Start with [Sprint_01/AUTH-001.md](Sprint_01/AUTH-001.md) — Bootstrap Zorovex Backend.

Nothing else until AUTH-001 is done.
