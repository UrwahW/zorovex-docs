# AUTH-003 — JWT Auth Middleware

| Field | Value |
|-------|-------|
| Sprint | 01 |
| Area | Backend |
| Status | Todo |

## Goal

Protect API routes with middleware that validates JWTs and attaches the authenticated user to the request context.

## Acceptance Criteria

- [ ] Middleware extracts Bearer token from `Authorization` header
- [ ] Invalid, expired, or missing token returns 401
- [ ] Valid token attaches `userId` (and role if present) to request context
- [ ] Protected routes reject unauthenticated requests
- [ ] Public routes (`/auth/register`, `/auth/login`) remain unprotected
- [ ] Middleware behavior documented in `03_Backend/AUTHENTICATION.md`

## Docs

**Read:** `03_Backend/AUTHENTICATION.md`, `02_Architecture/PERMISSIONS.md`

**Update:** `03_Backend/AUTHENTICATION.md`

## Cursor Prompt

Implement AUTH-003: JWT Auth Middleware.

Read `@09_Cursor/Cursor_Rules.md` and `@03_Backend/AUTHENTICATION.md`. AUTH-002 must be complete.

Add JWT validation middleware for protected routes. Document which routes are public vs protected. Add tests per `@09_Cursor/Sprint_01/AUTH-003.md`.
