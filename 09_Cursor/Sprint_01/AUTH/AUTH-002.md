# AUTH-002 — Login and JWT Issuance

| Field | Value |
|-------|-------|
| Sprint | 01 |
| Area | Backend |
| Status | Todo |

## Goal

Implement login so registered users receive a signed JWT for authenticated API access.

## Acceptance Criteria

- [ ] `POST /auth/login` accepts email and password
- [ ] Valid credentials return a signed JWT with user id and expiry
- [ ] Invalid credentials return 401 without revealing whether email exists
- [ ] JWT secret loaded from environment config (not hardcoded)
- [ ] Token payload documented in `03_Backend/AUTHENTICATION.md`
- [ ] Test covers valid login, wrong password, and unknown email

## Docs

**Read:** `03_Backend/AUTHENTICATION.md`, `02_Architecture/SECURITY.md`

**Update:** `03_Backend/AUTHENTICATION.md`, `03_Backend/API.md`

## Cursor Prompt

Implement AUTH-002: Login and JWT Issuance.

Read `@09_Cursor/Cursor_Rules.md` and `@03_Backend/AUTHENTICATION.md` first. AUTH-001 must be complete.

Build `POST /auth/login` with secure credential verification and JWT signing. Document token claims and expiry. Add tests per `@09_Cursor/Sprint_01/AUTH-002.md`.
