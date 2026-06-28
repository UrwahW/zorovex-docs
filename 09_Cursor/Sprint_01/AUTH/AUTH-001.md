# AUTH-001 — User Registration API

| Field | Value |
|-------|-------|
| Sprint | 01 |
| Area | Backend |
| Status | Todo |

## Goal

Implement user registration so a business owner can create an account with email and password.

## Acceptance Criteria

- [ ] `POST /auth/register` accepts email, password, and name
- [ ] Password is hashed before storage (never stored in plain text)
- [ ] Duplicate email returns a clear validation error
- [ ] Successful registration returns user id (no password in response)
- [ ] Endpoint documented in `03_Backend/AUTHENTICATION.md`
- [ ] Unit or integration test covers happy path and duplicate email

## Docs

**Read:** `03_Backend/AUTHENTICATION.md`, `03_Backend/DATABASE.md`, `02_Architecture/SECURITY.md`

**Update:** `03_Backend/AUTHENTICATION.md`, `03_Backend/API.md`

## Cursor Prompt

Implement AUTH-001: User Registration API.

Read `@09_Cursor/Cursor_Rules.md`, `@03_Backend/AUTHENTICATION.md`, and `@03_Backend/DATABASE.md` first.

Build `POST /auth/register` with email/password/name validation, secure password hashing, and duplicate-email handling. Document the endpoint and add tests per the acceptance criteria in `@09_Cursor/Sprint_01/AUTH-001.md`.
