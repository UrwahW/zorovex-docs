# Cursor Rules

How to use this repository with Cursor agents.

## Documentation-first

1. Read the relevant doc in `03_Backend/`, `04_Frontend/`, or `02_Architecture/` before writing code.
2. If the doc is missing detail, update the doc first, then implement.
3. Never implement behavior that contradicts an approved doc.

## Task workflow

1. Open the sprint folder under `09_Cursor/` (e.g. `Sprint_01/`).
2. Pick a task file (e.g. `AUTH-001.md`).
3. Paste the **Cursor Prompt** section into the agent, or reference the file with `@09_Cursor/Sprint_01/AUTH-001.md`.
4. Complete all **Acceptance Criteria** before marking the task done.
5. Update linked documentation and add an entry to `00_Project/CHANGELOG.md` when the task ships.

## Agent instructions

When working on a Cursor task:

- Follow `02_Architecture/CODING_STANDARDS.md` and `02_Architecture/TECH_STACK.md`.
- Respect RBAC and multi-tenancy from `02_Architecture/PERMISSIONS.md`.
- Keep changes scoped to the task — do not refactor unrelated code.
- Write or update tests listed in the task's acceptance criteria.
- Cross-link related docs in each file's **Related Docs** section.

## Task file format

Each task under `09_Cursor/Sprint_XX/` includes:

| Section | Purpose |
|---------|---------|
| Goal | What the task delivers |
| Acceptance Criteria | Checklist for done |
| Docs | What to read and what to update |
| Cursor Prompt | Ready-to-run agent instruction |

## Naming convention

`{AREA}-{NNN}.md`

| Prefix | Area |
|--------|------|
| AUTH | Authentication and authorization |
| ORG | Organizations and multi-tenancy |
| UI | Frontend screens and layout |
| BUS | Business setup and onboarding |
| API | General API endpoints |
| DB | Database schema and migrations |

## Sprint mapping

| Folder | Sprint doc |
|--------|------------|
| `Sprint_01/` | [Sprint_01.md](../08_Sprints/Sprint_01.md) |
| `Sprint_02/` | [Sprint_02.md](../08_Sprints/Sprint_02.md) |
| `Sprint_03/` | [Sprint_03.md](../08_Sprints/Sprint_03.md) |
| `Sprint_04/` | — |
