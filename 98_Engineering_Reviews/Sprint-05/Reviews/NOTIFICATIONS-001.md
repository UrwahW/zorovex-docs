# NOTIFICATIONS-001 — Engineering Review

**Task:** NOTIFICATIONS-001 (Notification Center)
**Sprint:** Sprint 05
**Status:** Pending Architect Approval
**Depends On:** AUTO-001, COMMS-001, BOOK-001, CRM-003, AI-007

---

## Summary

Implemented a centralized Notification Center. All in-app notifications flow through `Notifications::NotificationService` with source, category, priority, grouping metadata, read/archive/snooze support, and user preferences. APIs are exposed at `/api/v1/notifications`. The dashboard header includes a notification bell; the full feed lives at `/notifications`. Legacy `/comms/notifications` redirects to the centralized page.

---

## Services Added

| Service | Purpose |
|---------|---------|
| `Notifications::NotificationService` | Create, read, archive, unread counts |
| `Notifications::PreferenceService` | Per-user delivery preferences and quiet hours |
| `Notifications::TemplateService` | Notification content templates |
| `Notifications::Dispatcher` | Organization-wide dispatch helper |
| `Notifications::HistoryService` | Feed listing with filters |
| `Notifications::EventLogger` | Structured notification audit logging |

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/v1/notifications` | Notification feed |
| PATCH | `/api/v1/notifications/:id` | Mark read, archive, snooze, mute |
| GET | `/api/v1/notifications/unread-count` | Unread badge count |
| PATCH | `/api/v1/notifications/read-all` | Mark all read |
| GET/PATCH | `/api/v1/notifications/preferences` | User notification preferences |

---

## Producers Migrated

| Module | Integration |
|--------|-------------|
| Communications | New message alerts with source/category/priority |
| Bookings | Appointment reminder and cancellation notifications |
| Workflows | Workflow expiration alerts |
| Automations | `create_notification` action |

`Comms::NotificationService` remains as a thin delegate for backward compatibility.

---

## Frontend

| Route / Component | Feature |
|-------------------|---------|
| `/notifications` | Centralized notification feed + preferences |
| `NotificationBell` | Header unread badge |
| `/comms/notifications` | Redirects to `/notifications` |

---

## Database

Extended `notifications` table with `priority`, `category`, `source`, `group_key`, `archived_at`, `snoozed_until`, `muted_at`, `deleted_at`.

New `notification_preferences` table for per-user settings.

---

## Tests

- `spec/requests/notifications_center_spec.rb`

---

## Notes / Follow-ups

- External delivery channels (email, push, WhatsApp) are preference-ready but in-app only in this phase
- Organization-level default preferences are owner-managed; member-level overrides can be expanded
- AI runtime and payment modules can adopt `Notifications::Dispatcher` when those events land
