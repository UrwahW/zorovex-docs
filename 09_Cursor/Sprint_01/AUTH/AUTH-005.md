# AUTH-005 — Current User Endpoint

| Field | Value |
|-------|-------|
| Sprint | 01 |
| Area | Backend |
| Status | Todo |

## Goal

Provide `GET /auth/me` so the frontend can load the logged-in user's profile and active organization after login.

## Acceptance Criteria

- [ ] `GET /auth/me` requires valid JWT
- [ ] Returns user id, name, email, role, and active organization id
- [ ] Returns 401 when token is missing or invalid
- [ ] Response shape documented in `03_Backend/AUTHENTICATION.md` and `03_Backend/API.md`
- [ ] Test covers authenticated and unauthenticated requests

## Docs

**Read:** `03_Backend/AUTHENTICATION.md`, `03_Backend/ORGANIZATIONS.md`

**Update:** `03_Backend/AUTHENTICATION.md`, `03_Backend/API.md`

## Cursor Prompt

Implement AUTH-005: Current User Endpoint.

Read `@03_Backend/AUTHENTICATION.md`. AUTH-003 and ORG-002 must be complete.

Build `GET /auth/me` returning user profile and active org context. Document response schema and add tests per `@09_Cursor/Sprint_01/AUTH-005.md`.
