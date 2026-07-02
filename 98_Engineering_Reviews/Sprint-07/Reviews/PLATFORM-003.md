# PLATFORM-003 — Engineering Review

**Task:** PLATFORM-003 (Platform Administration & Support Workspace)  
**Sprint:** Sprint 07  
**Status:** Pending Architect Approval  
**Depends On:** PLATFORM-001, PLATFORM-002, CORE-001, SETTINGS-001, INTEGRATIONS-001

---

## Summary

Implemented the internal Platform Administration workspace for Zorovex staff. Platform administrators can browse customer organizations, start audited support sessions (read-only or full support), manage modules/features/subscriptions, and view aggregated organization health — without impersonating customer users. Support sessions preserve platform admin identity and switch organization context via `X-Platform-Support-Session` header.

---

## Backend Services

| Service | Purpose |
|---------|---------|
| `Platform::AuthorizationService` | Platform RBAC (administrator, support, billing, developer) |
| `Platform::SupportSessionService` | Create/end/expire support sessions with audit trail |
| `Platform::WorkspaceAccessService` | Workspace permission payload for support sessions |
| `Platform::OrganizationDirectoryService` | Paginated organization directory with health signals |
| `Platform::OrganizationAdminService` | Org detail, modules, features, subscription, AI controls |
| `Platform::OrganizationHealthAdminService` | AI, provider, automation, escalation health aggregation |
| `Platform::ModuleRegistry` | Product module → feature entitlement mapping |

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/v1/platform/organizations` | Organization directory (search, filters, pagination) |
| GET | `/api/v1/platform/organizations/:id` | Organization detail, health, sessions, entitlements |
| POST | `/api/v1/platform/organizations/:id/support` | Start support session (reason required) |
| POST | `/api/v1/platform/organizations/:id/end_support` | End active support session |
| PATCH | `/api/v1/platform/organizations/:id/modules` | Enable/disable product modules |
| PATCH | `/api/v1/platform/organizations/:id/features` | Feature flags + AI controls |
| PATCH | `/api/v1/platform/organizations/:id/subscription` | Suspend/reactivate/cancel/plan changes (`operation` param) |

---

## Auth & Support Sessions

- Platform staff authenticated via JWT; **no user impersonation**
- `X-Platform-Support-Session` header sets `Current.organization` from active session
- Platform admin identity preserved in `Current.user` for all actions
- Customer organizations see active support session via `/api/v1/me` (`active_support_session`)
- Session timeout: 2 hours (auto-expire + audit)

---

## Permissions

| Role | Access |
|------|--------|
| Platform Administrator (`super_admin` or `platform_role: administrator`) | Full access |
| Platform Support | Read-only support sessions only |
| Billing Team | Subscription controls only |
| Developer | Read-only directory/detail |

---

## Frontend

| Route | Feature |
|-------|---------|
| `/platform/admin` | Organization directory |
| `/platform/admin/organizations/:id` | Org detail, support panel, modules, features, subscription, health |

Nav item **Platform Admin** visible only to `platform_staff` users.

---

## Database

| Change | Purpose |
|--------|---------|
| `platform_support_sessions` | Support session records |
| `users.platform_role` | Platform staff RBAC |
| `organizations.ai_paused`, `ai_actions_disabled`, `force_human_only` | AI control flags |

---

## Audit

All support session lifecycle events and configuration changes recorded via `Audit::AuditEventService` with `module_name: platform` and platform admin attribution metadata.

---

## Tests

- `spec/requests/platform_administration_spec.rb` — 11 examples (directory, detail, support, modules, features, subscription, workspace access, permissions)
- `spec/services/platform/super_admin_service_spec.rb` — existing specs pass with updated authorization

Run:

```bash
DATABASE_URL=postgres://zorovex:zorovex@localhost:5432/zorovex_test \
REDIS_URL=redis://localhost:6379/0 \
bundle exec rspec spec/requests/platform_administration_spec.rb
```

---

## Notes / Follow-ups

- Subscription PATCH uses `operation` (not `action`) to avoid Rails param collision
- Marketing/inventory/POS modules registered but have no feature mappings yet (future)
- Support session write-guard policy hook (`write_via_support_session?`) ready for controller integration on customer mutation endpoints
- Dedicated platform admin audit explorer can reuse `/audit` with platform module filter in a follow-up

---

**Stopped for architect approval.**
