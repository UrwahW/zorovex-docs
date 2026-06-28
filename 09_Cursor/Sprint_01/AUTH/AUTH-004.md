# AUTH-004 — Roles and RBAC Seed

| Field | Value |
|-------|-------|
| Sprint | 01 |
| Area | Backend |
| Status | Todo |

## Goal

Define initial roles (owner, admin, staff) and enforce role-based access on organization-scoped endpoints.

## Acceptance Criteria

- [ ] Roles table/enum seeded with `owner`, `admin`, `staff`
- [ ] New organization creator is assigned `owner` role
- [ ] Role is included in JWT or resolvable from user + org context
- [ ] At least one protected endpoint checks role (e.g. only owner can delete org)
- [ ] Role matrix documented in `02_Architecture/PERMISSIONS.md`
- [ ] Tests cover allowed and denied role access

## Docs

**Read:** `02_Architecture/PERMISSIONS.md`, `03_Backend/AUTHENTICATION.md`, `03_Backend/ORGANIZATIONS.md`

**Update:** `02_Architecture/PERMISSIONS.md`, `03_Backend/AUTHENTICATION.md`

## Cursor Prompt

Implement AUTH-004: Roles and RBAC Seed.

Read `@02_Architecture/PERMISSIONS.md` and `@03_Backend/ORGANIZATIONS.md`. AUTH-003 must be complete.

Seed owner/admin/staff roles, assign owner on org creation, and enforce RBAC on at least one endpoint. Document the role matrix per `@09_Cursor/Sprint_01/AUTH-004.md`.
