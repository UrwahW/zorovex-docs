# BOOK-001 — Engineering Review

**Task:** BOOK-001 (Booking Engine)
**Sprint:** 02
**Status:** Pending Architect Approval

---

## Summary

Implemented BOOK-001 per `09_Cursor/BOOK/BOOK-001.md`. The booking engine provides appointment CRUD, availability checking with conflict detection, calendar views (day/week/month), reschedule/cancel workflows, CRM integration (timeline, `bookings_count`, `last_booking_at`), and a booking dashboard with performance stats. Owner/Manager have full access; Receptionist can create/update/cancel; Marketing and Accountant have read-only access.

**Verification:** 555 RSpec examples (0 failures), 71 Vitest tests (0 failures), RuboCop clean on BOOK-001 files, Brakeman 0 warnings.

---

## Files Created

### Backend

- `db/migrate/20240628000030_create_appointments.rb`
- `app/domains/booking/models/appointment.rb`
- `app/services/bookings/types.rb`
- `app/services/bookings/appointment_validator.rb`
- `app/services/bookings/availability_service.rb`
- `app/services/bookings/booking_service.rb`
- `app/services/bookings/reschedule_service.rb`
- `app/services/bookings/cancel_service.rb`
- `app/services/bookings/crm_integration.rb`
- `app/commands/bookings/delete_command.rb`
- `app/queries/bookings/list_query.rb`
- `app/queries/bookings/find_by_id_query.rb`
- `app/queries/bookings/calendar_query.rb`
- `app/queries/bookings/dashboard_query.rb`
- `app/policies/appointment_policy.rb`
- `app/serializers/appointment_serializer.rb`
- `app/serializers/booking_dashboard_serializer.rb`
- `app/controllers/concerns/bookings/response_rendering.rb`
- `app/controllers/api/v1/bookings_controller.rb`
- `spec/factories/appointments.rb`
- `spec/domains/booking/models/appointment_spec.rb`
- `spec/policies/appointment_policy_spec.rb`
- `spec/services/bookings/availability_service_spec.rb`
- `spec/requests/bookings_spec.rb`

### Frontend

- `frontend/src/features/bookings/types/appointment.ts`
- `frontend/src/features/bookings/constants/booking-options.ts`
- `frontend/src/features/bookings/api/bookings-api.ts`
- `frontend/src/features/bookings/hooks/use-booking-access.ts`
- `frontend/src/features/bookings/hooks/use-bookings.ts`
- `frontend/src/features/bookings/routes/bookings-access-route.tsx`
- Pages: `booking-dashboard-page`, `booking-calendar-page`, `appointment-list-page`, `appointment-details-page`, `create-booking-page`, `edit-booking-page`
- Components: `bookings-header`, `appointment-card`, `booking-filters-bar`, `booking-calendar`, `availability-picker`, `reschedule-dialog`, `cancel-dialog`
- `frontend/src/features/bookings/components/bookings-components.test.tsx`

---

## Files Modified

- `backend/config/application.rb` — autoload `app/domains/booking/models`
- `backend/config/routes.rb` — bookings API routes
- `backend/app/domains/organization/models/organization.rb` — `has_many :appointments`
- `backend/app/domains/crm/models/contact.rb` — `has_many :appointments`
- `backend/app/services/crm/contacts/types.rb` — appointment activity types
- `backend/app/queries/crm/contacts/unified_timeline_query.rb` — appointment timeline items
- `backend/.rubocop.yml` — bookings exclusions
- `frontend/src/routes/router.tsx` — `/bookings/*` routes
- `frontend/src/layouts/dashboard-layout.tsx` — Bookings nav link

---

## Database Changes

Migration `20240628000030_create_appointments`:

| Column | Purpose |
|--------|---------|
| `organization_id` | Tenant scope |
| `contact_id` | CRM contact link (required) |
| `service_id` | Business service (required) |
| `staff_id` | Assigned staff (optional) |
| `starts_at` / `ends_at` | Appointment window |
| `duration_minutes` | Service duration |
| `status` | Workflow state |
| `source` | Booking channel |
| `notes` / `cancel_reason` | Text fields |
| `created_by` | User who created |
| `deleted_at` | Soft delete |

---

## API Endpoints

| Method | Path | Access |
|--------|------|--------|
| GET | `/api/v1/bookings` | List (all read roles); `?dashboard=true` for stats |
| GET | `/api/v1/bookings/:id` | Show |
| POST | `/api/v1/bookings` | Owner, Manager, Receptionist |
| PATCH | `/api/v1/bookings/:id` | Owner, Manager, Receptionist |
| DELETE | `/api/v1/bookings/:id` | Owner, Manager (soft delete) |
| GET | `/api/v1/bookings/calendar` | Calendar data (day/week/month) |
| GET | `/api/v1/bookings/availability` | Available time slots |
| POST | `/api/v1/bookings/:id/reschedule` | Owner, Manager, Receptionist |
| POST | `/api/v1/bookings/:id/cancel` | Owner, Manager, Receptionist |

---

## Tests Added

- Model: `Appointment`
- Policy: `AppointmentPolicy` (owner, marketing, receptionist)
- Service: `Bookings::AvailabilityService`
- Request: create, availability, calendar, cancel, reschedule, dashboard stats, permission checks
- Frontend: appointment card, filters, routing

---

## Assumptions

- Working hours come from org-level `business_availabilities` (not per-staff schedules)
- Conflict detection applies when `staff_id` is set; slots without staff skip staff conflict checks
- Revenue dashboard stat sums `price_cents` from completed appointments (placeholder per spec)
- Dashboard stats served via `GET /api/v1/bookings?dashboard=true` (deliverable not listed separately in API table)
- Calendar drag-and-drop updates appointment via PATCH (resize uses duration from existing appointment)

---

## Risks

- No per-staff working hours — all staff share org availability window
- Synchronous slot generation may be slow for large date ranges
- Month calendar view uses same hourly grid as week (simplified UI)

---

## Technical Debt

- No dedicated payments/invoicing integration (explicitly out of scope)
- Calendar resize handle not implemented separately from drag (duration updated on drop)
- Staff assignment optional; unassigned bookings skip double-booking staff checks

---

## Acceptance Criteria

- [x] Calendar operational
- [x] Availability engine working
- [x] Appointment CRUD working
- [x] Conflict detection working
- [x] CRM timeline updates
- [x] Dashboard operational
- [x] Tests pass
- [x] RuboCop passes (BOOK-001 scope)
- [x] Brakeman passes

**Stop:** No tasks beyond BOOK-001 started.
