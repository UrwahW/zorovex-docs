# AUDIT-001 — Engineering Review

**Task:** AUDIT-001 (Audit & Activity Platform)
**Sprint:** Sprint 05
**Status:** Pending Architect Approval
**Depends On:** AUTO-001, NOTIFICATIONS-001

---

## Summary

Implemented a centralized Audit Platform with append-only `audit_events` records. Every meaningful action can be traced with organization, actor, entity, severity, correlation/request IDs, and request metadata. Activity timelines support entity, user, and organization views. CSV and JSON export are available. Frontend dashboard at `/audit`.

---

## Services Added

| Service | Purpose |
|---------|---------|
| `Audit::AuditEventService` | Append-only audit event recorder |
| `Audit::AuditService` | Filtered audit listing with RBAC module scoping |
| `Audit::TimelineService` | Entity, user, organization, customer, booking, conversation, workflow timelines |
| `Audit::AuditExporter` | CSV and JSON export |
| `Audit::RetentionService` | 7-year default soft archive |
| `Audit::EventLogger` | Structured audit logging |

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/v1/audit` | List audit events with filters |
| GET | `/api/v1/audit/:id` | Single audit event |
| GET | `/api/v1/audit/entity/:id` | Entity timeline |
| GET | `/api/v1/audit/user/:id` | User activity history |
| GET | `/api/v1/audit/organization` | Organization timeline |
| GET | `/api/v1/audit/export` | Export CSV or JSON |

---

## Producers Wired

| Module | Events |
|--------|--------|
| Authentication | `user_login`, `user_logout` |
| CRM | `contact_created` |
| Automations | All automation lifecycle events |
| Notifications | Notification created/read/archived |
| Exports | `audit_exported` |

---

## Frontend

| Route | Feature |
|-------|---------|
| `/audit` | Audit dashboard, filters, CSV/JSON export |

---

## Permissions

| Role | Access |
|------|--------|
| Owner | Full read + export |
| Manager | Full read + export |
| Receptionist | Limited modules (CRM, bookings, communications) |
| Marketing | CRM, communications, AI, automations, notifications |
| Accountant | Financial modules only + export |

---

## Database

`audit_events` — immutable append-only table with soft archive via `archived_at`.

---

## Tests

- `spec/requests/audit_spec.rb`
- `spec/services/audit/audit_event_service_spec.rb`
- `spec/services/audit/retention_service_spec.rb`

---

## Notes / Follow-ups

- Excel and PDF export formats deferred; CSV and JSON implemented
- Additional module producers (payments, calendar, AI runtime) can adopt `Audit::AuditEventService`
- Retention archival job can be scheduled via ActiveJob in a future task
