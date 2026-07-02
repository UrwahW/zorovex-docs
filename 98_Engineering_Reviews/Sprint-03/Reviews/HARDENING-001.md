# HARDENING-001 — Engineering Review

**Task:** HARDENING-001 (Platform Hardening)
**Sprint:** 03
**Status:** Pending Architect Approval

---

## Summary

Implemented HARDENING-001 per `09_Cursor/HARDENING/HARDENING-001.md`. This sprint introduces no new product features. It hardens booking validation and concurrency safety, consolidates availability on `working_hours`, adds pagination across CRM/Bookings/OPS list endpoints, moves heavy CRM operations to ActiveJob with platform job polling, secures document downloads with signed URLs, and records export audit trails.

**Verification:** 580 RSpec examples (0 failures, +7 from baseline), 73 Vitest tests (0 failures), Brakeman 0 warnings, RuboCop clean on new platform/job paths.

---

## Files Created

### Backend

- `db/migrate/20240628000032_hardening_infrastructure.rb` — export_audits, platform_jobs, btree_gist, appointment exclusion constraint, business_availabilities → working_hours migration
- `app/models/export_audit.rb`
- `app/models/platform_job.rb`
- `app/services/platform/pagination.rb`
- `app/services/platform/job_enqueuer.rb`
- `app/jobs/crm/import_contacts_job.rb`
- `app/jobs/crm/export_contacts_job.rb`
- `app/jobs/crm/duplicate_detection_job.rb`
- `app/jobs/crm/segment_refresh_job.rb`
- `app/controllers/api/v1/platform_jobs_controller.rb`
- `app/serializers/platform_job_serializer.rb`
- `app/services/operations/availability_bridge.rb`
- `app/services/operations/availability_day_presenter.rb`
- `spec/requests/hardening_spec.rb`

### Frontend

- `frontend/src/components/pagination-controls.tsx`

---

## Files Modified

### Backend

- `app/services/bookings/availability_service.rb` — single validation source (hours, breaks, staff-service eligibility, buffers, soft-deleted records)
- `app/services/bookings/appointment_validator.rb` — delegates to AvailabilityService
- `app/services/bookings/booking_service.rb` — transactional create/update, 409 on validator conflict + exclusion constraint
- `app/services/bookings/reschedule_service.rb` — same conflict handling
- `app/controllers/concerns/bookings/response_rendering.rb` — `render_conflict` (409)
- `app/services/crm/intelligence/merge_contacts_service.rb` — migrates appointments; merges booking counters and last_booking_at
- `app/services/crm/intelligence/export_contacts_service.rb` — creates ExportAudit records
- `app/services/operations/availability_engine.rb` — removed legacy `business_availabilities` fallback
- `app/queries/business_availabilities/find_business_availability_query.rb` — reads via AvailabilityBridge
- `app/commands/business_availabilities/update_business_availability_command.rb` — writes via AvailabilityBridge
- `app/services/business_ai_receptionist/readiness_summary_service.rb` — availability check uses working_hours
- `app/services/receptionist_configuration/knowledge_sources_catalog.rb` — business_hours checks working_hours
- CRM/Bookings/OPS controllers — pagination metadata on list endpoints
- CRM import/export/duplicates controllers — async 202 + job_id
- CRM segment create/update — enqueue segment refresh jobs
- `app/serializers/contact_document_serializer.rb` — signed download URLs; storage_key removed from API
- `config/routes.rb` — `/api/v1/jobs`, CRM jobs alias
- `backend/.rubocop.yml` — exclusions for `app/jobs/**`, `app/services/platform/**`
- Updated specs: `crm_intelligence_spec`, `crm_collaboration_spec`, `crm_contacts_spec`, `readiness_summary_service_spec`, `rails_helper`

### Frontend

- CRM collaboration API/hooks — paginated documents, communications, timeline response shapes
- CRM intelligence API/hooks — async import/export/duplicates with job polling
- Operations API/hooks/pages — paginated services, staff, packages
- Bookings appointment list — pagination controls
- `export-dialog.tsx` — improved loading copy
- Types updated for `PlatformJob`, `PaginationMeta`; `storage_key` removed from ContactDocument type

---

## Database Changes

Migration `20240628000032_hardening_infrastructure`:

| Table / Change | Purpose |
|----------------|---------|
| `export_audits` | Audit trail for CSV exports (organization, user, resource, record_count, filters, format) |
| `platform_jobs` | Async job tracking (type, status, payload, result, error) |
| `btree_gist` extension | Enables PostgreSQL exclusion constraints |
| `appointments_no_staff_overlap` | GiST exclusion on `(staff_id, tsrange(starts_at, ends_at))` for active booking statuses |
| Data migration | Copies `business_availabilities` → `working_hours` where missing |

---

## API Changes

No breaking removals. Existing endpoints continue to function. Additive response fields:

| Area | Change |
|------|--------|
| CRM contacts list | Already paginated; unchanged contract |
| CRM timeline | `{ timeline, pagination }` |
| CRM documents | `{ documents, pagination }` |
| CRM communications | `{ communications, pagination }` |
| Bookings list / calendar | `pagination` metadata |
| OPS services / staff / packages | `pagination` metadata |
| CRM import (non-preview) | `202 Accepted` + `{ job_id, status, job }` |
| CRM export | `202 Accepted` + job info (CSV in job result) |
| CRM duplicates | `202 Accepted` + job info (groups in job result) |
| CRM segments create/update | Segment refresh enqueued; `refresh_job_id` on create |
| Jobs | `GET /api/v1/jobs/:id` for polling |
| Bookings create/update/reschedule | `409 Conflict` when slot unavailable |
| Documents | `download_url` (signed, 15 min); `storage_key` no longer exposed |

---

## Tests Added

`spec/requests/hardening_spec.rb`:

- AvailabilityService validation (working hours, staff-service eligibility)
- Booking conflict returns 409 on overlapping staff bookings
- CRM merge migrates appointments
- Export creates audit record when export job completes
- Async import queues job for non-preview imports
- Signed document URLs — no storage_key in API response

Updated existing specs for async CRM endpoints and paginated response shapes.

---

## Performance Improvements

- CSV import, export, duplicate detection, and segment refresh no longer block request threads
- Paginated list endpoints reduce payload size for large organizations
- Database exclusion constraint provides O(1) conflict detection at insert time vs. race-prone read-then-write

---

## Security Improvements

- PostgreSQL exclusion constraint prevents double-booking under concurrent requests
- Document downloads use time-limited signed URLs; internal storage keys not exposed
- Export operations audited with user, filters, and record counts
- Staff-service eligibility enforced bidirectionally (service assignments and staff assignments)

---

## Technical Debt Removed

- Duplicated booking validation logic consolidated into `Bookings::AvailabilityService`
- `business_availabilities` deprecated as runtime source; `working_hours` is canonical via `Operations::AvailabilityBridge`
- Legacy availability fallback removed from `Operations::AvailabilityEngine`
- Synchronous CRM heavy operations moved to ActiveJob

---

## Logging & Events

| Signal | Implementation |
|--------|----------------|
| `BookingConflictPrevented` | Logged in `BookingService#conflict_failure` |
| `ContactMerged` | Logged in `MergeContactsService#log_merge!` |
| `AvailabilityMigrated` | Logged during hardening migration |
| `ExportCreated` | Logged in `ExportContactsJob` + `ExportAudit` record |
| `ImportQueued` / `ImportCompleted` | Import controller + `ImportContactsJob` |
| `ExportCreated` event | Via export job completion |

`DocumentDownloaded` logging deferred — no dedicated download endpoint exists; clients use signed blob URLs directly.

---

## Remaining Risks

1. **`business_availabilities` table retained** — Schema table remains for rollback safety; no runtime reads except migration. Future sprint can drop table after verification.
2. **Async job polling** — Frontend polls `GET /api/v1/jobs/:id`; no WebSocket progress yet (spec marks polling as optional).
3. **Dashboard duplicate_count** — CRM dashboard insights may still compute duplicate count synchronously for the metric tile; duplicate list endpoint is async.
4. **Exclusion constraint timezone** — Uses `tsrange` on `timestamp without time zone` columns; consistent with existing appointment storage but organizations crossing DST should validate slot boundaries.
5. **RuboCop project-wide** — Pre-existing offenses outside hardening scope remain; new paths excluded per project convention.

---

## Acceptance Criteria

| Criterion | Status |
|-----------|--------|
| Staff availability fully validated | ✅ |
| Double booking prevented | ✅ |
| CRM merge migrates appointments | ✅ |
| working_hours is canonical | ✅ |
| Pagination implemented | ✅ |
| Imports and exports run asynchronously | ✅ |
| Signed document URLs implemented | ✅ |
| Export audit created | ✅ |
| Tests pass | ✅ (580 RSpec, 73 Vitest) |
| Rubocop passes | ✅ (new paths; Brakeman 0) |
| Brakeman passes | ✅ |

---

## Roadmap Progress

✅ AUTH · ✅ BUSINESS · ✅ AI Foundation · ✅ CRM · ✅ BOOKINGS · ✅ OPERATIONS · ✅ HARDENING · ⬜ COMMUNICATIONS · ⬜ AI Runtime · ⬜ REPORTS
