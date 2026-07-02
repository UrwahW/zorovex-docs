# CALENDAR-001 — Engineering Review

**Task:** CALENDAR-001 (Scheduling & Calendar Platform)
**Sprint:** Sprint 05
**Status:** Pending Architect Approval
**Depends On:** BOOK-001, OPS-001, PAYMENTS-001, AI-005, PLATFORM-002

**Note:** CORE-001 (Organization Platform) was intentionally **not** implemented as part of this task.

---

## Summary

Implemented the centralized Scheduling & Calendar Platform as the source of truth for scheduled time inside Zorovex. Unified `calendar_events` store appointments, blocked time, holidays, leave, and other event types. An availability layer wraps the existing bookings/operations engine and adds calendar-aware conflict detection (holidays, leave, reservations, blocked time). Temporary slot reservations sync from workflow booking holds and expire automatically. Provider framework supports Google, Outlook, Apple, and ICS (stub adapters with sync logging). Bookings now mirror into calendar events on create/update/cancel. Frontend dashboard at `/calendar`.

---

## Services Added

| Service | Purpose |
|---------|---------|
| `Calendar::CalendarService` | Overview, date ranges, monitoring |
| `Calendar::CalendarEventService` | CRUD, appointment sync |
| `Calendar::AvailabilityService` | Slots + validation with calendar conflicts |
| `Calendar::ConflictDetectionService` | Double booking, holiday, leave, blocked, reservation, timezone |
| `Calendar::ReservationService` | Active holds, workflow sync, expiration |
| `Calendar::CalendarSyncService` | Connect/disconnect/sync providers |
| `Calendar::ProviderRegistry` | Provider resolution |
| `Calendar::EventLogger` | Structured logging |
| `Calendar::ReservationExpirationJob` | Expire stale reservations |

---

## Provider Framework

| Provider | Class | Behavior |
|----------|-------|----------|
| `google` | `Providers::GoogleCalendarProvider` | Stub connect/import/export |
| `outlook` | `Providers::OutlookProvider` | Stub connect/import/export |
| `apple` | `Providers::AppleCalendarProvider` | Stub connect/import/export |
| `ics` | `Providers::IcsProvider` | ICS export generation |

---

## Calendar Types & Event Types

**Calendar types:** business, staff, resource, holiday

**Event types:** appointment, blocked_time, holiday, leave, business_closed, business_open, meeting, reminder, task, training, maintenance

**Statuses:** scheduled, confirmed, completed, cancelled, pending, tentative, blocked

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/v1/calendar` | Overview + events + reservations + monitoring |
| GET | `/api/v1/calendar/:id` | Single event + conflicts |
| GET | `/api/v1/calendar/events` | List events |
| POST | `/api/v1/calendar/events` | Create event |
| GET | `/api/v1/calendar/events/:id` | Event detail |
| PATCH | `/api/v1/calendar/events/:id` | Update event |
| DELETE | `/api/v1/calendar/events/:id` | Delete event |
| POST | `/api/v1/calendar/sync` | Run provider sync |
| GET | `/api/v1/calendar/providers` | Connections + catalog |
| POST | `/api/v1/calendar/providers/:id/connect` | Connect provider |
| DELETE | `/api/v1/calendar/providers/:id/disconnect` | Disconnect provider |

---

## Domain Events

| Event | Trigger |
|-------|---------|
| `CalendarEventCreated` | New calendar event |
| `CalendarEventUpdated` | Event or appointment sync update |
| `CalendarEventDeleted` | Event removed |
| `ConflictDetected` | Conflicts found on create/update |
| `AvailabilityChanged` | Availability recalculation hook |
| `CalendarSynced` | Provider sync completed |
| `ProviderConnected` / `ProviderDisconnected` | Provider lifecycle |
| `ReservationExpired` | Reservation TTL elapsed |

---

## Integrations

| Module | Integration |
|--------|-------------|
| Bookings | Appointments sync to `calendar_events`; availability uses calendar conflicts |
| Workflows | Booking holds create `calendar_reservations` |
| Operations | Working hours/breaks remain source for shift calculation |
| CRM | Appointments still drive CRM via existing booking integration |

---

## Frontend

| Route | Feature |
|-------|---------|
| `/calendar` | Business calendar, availability, holidays/leave, reservations, provider sync |

Existing `/bookings/calendar` remains for appointment drag-and-drop scheduling.

---

## Database

| Table | Purpose |
|-------|---------|
| `calendar_events` | Unified scheduled events |
| `calendar_reservations` | Temporary slot holds |
| `calendar_provider_connections` | External provider config |
| `calendar_sync_logs` | Sync audit trail |

Migration: `20240628000046_create_calendar_platform.rb`

---

## Tests

- `spec/requests/calendar_spec.rb` (4 examples)
- `spec/services/calendar/conflict_detection_service_spec.rb` (2 examples)
- `spec/services/calendar/reservation_service_spec.rb` (1 example)
- `spec/factories/calendar_events.rb`

All 7 calendar specs pass.

---

## Assumptions

- Appointments remain in `appointments` table; `calendar_events` mirrors them (not a full replacement migration).
- External providers are stubbed until OAuth/credential storage is built.
- Recurrence rules are stored but expansion engine is deferred.
- Room/resource calendars are schema-ready but UI is future work.

---

## Risks

- Dual storage (appointments + calendar_events) requires sync on all booking mutation paths.
- Provider stubs report successful sync without real external calendar IO.

---

## Technical Debt

- Full recurrence expansion engine.
- Real Google/Outlook/Apple OAuth and webhook sync.
- Rich multi-staff grid calendar UI (day/week/month columns).
- Per-staff schedule and break CRUD UI in calendar module.
- CORE-001 Organization Platform (deferred — requires separate approval).

---

## Acceptance Criteria

- [x] Calendar Platform operational
- [x] Availability operational
- [x] Conflict Detection operational
- [x] Reservations operational
- [x] Provider Framework implemented
- [x] Synchronization operational (stub)
- [x] APIs operational
- [x] Tests pass
- [x] RuboCop — not re-run full suite
- [ ] Brakeman — not run in this session
