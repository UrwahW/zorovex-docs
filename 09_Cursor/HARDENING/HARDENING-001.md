# ENGINEERING TASK

ID

HARDENING-001

Sprint

Sprint 3

Title

Platform Hardening

Status

Approved

Depends On

CRM-003

BOOK-001

OPS-001

---

# Objective

Strengthen the platform before implementing the AI Runtime.

This task introduces no user-facing features.

Its purpose is to improve correctness, consistency, concurrency safety, security and production readiness.

---

# Scope

Implement

- Booking Validation Hardening
- Atomic Booking Conflicts
- CRM Merge Improvements
- Availability Consolidation
- Pagination
- Async Processing
- Secure Document Access
- Export Audit Logging

No new business features.

---

# 1. Booking Validation

Update AppointmentValidator.

Booking creation must validate

- Staff working hours
- Staff breaks
- Staff-service eligibility
- Service buffer_before
- Service buffer_after
- Soft deleted services
- Soft deleted staff

AvailabilityService becomes the single validation source.

Remove duplicated validation logic.

---

# 2. Booking Race Conditions

Prevent double bookings under concurrent requests.

Implementation may use

- database exclusion constraint

or

- transaction with row locking

Conflict detection and booking creation must execute atomically.

Return

409 Conflict

when simultaneous booking attempts collide.

---

# 3. CRM Merge

MergeContactsService must also migrate

- Appointments
- Timeline
- Booking counters
- Last booking date

After merge

No orphaned appointments may exist.

All related records must reference the surviving contact.

---

# 4. Availability Consolidation

working_hours becomes the canonical availability source.

Tasks

- migrate existing business_availabilities
- update booking services
- update availability engine
- update APIs
- update documentation

Deprecate business_availabilities.

No future code should depend on it.

---

# 5. Pagination

Add pagination to

CRM

- Contacts
- Timeline
- Documents
- Communications

Bookings

- Appointment List
- Calendar queries

Operations

- Services
- Staff
- Packages

Use existing pagination conventions.

---

# 6. Async Processing

Move to ActiveJob

- CSV Import
- CSV Export
- Duplicate Detection
- Segment Refresh

API must immediately return job information.

Progress polling is optional.

---

# 7. Secure Documents

Replace permanent document URLs.

Use signed URLs.

Respect existing storage provider abstraction.

Validate

- MIME type
- Maximum file size

Do not expose storage paths.

---

# 8. Export Audit

Create

export_audits

Columns

id

organization_id

user_id

resource

record_count

filters

export_format

created_at

Every export operation must create an audit record.

---

# Backend

Update

AppointmentValidator

AvailabilityService

BookingService

MergeContactsService

ImportContactsService

ExportContactsService

SegmentEngine

DocumentService

Pagination helpers

---

# API

No breaking API changes.

Existing endpoints continue to function.

Responses may include

pagination

metadata

job_id

where applicable.

---

# Frontend

Update

CRM Lists

Booking Lists

Operations Lists

Document Downloads

Import UI

Export UI

Loading States

Pagination Controls

No redesign.

---

# Permissions

Preserve existing permissions.

No RBAC changes.

---

# Logging

BookingConflictPrevented

ContactMerged

AvailabilityMigrated

ExportCreated

ImportQueued

DocumentDownloaded

---

# Events

BookingConflictPrevented

ExportCreated

ImportCompleted

---

# Out of Scope

AI Runtime

Tool Calling

WhatsApp

Voice

Reports

Analytics

Memory

Prompt Compiler

Provider Integrations

---

# Testing

Create

Concurrency Specs

Booking Validation Specs

Merge Specs

Migration Specs

Pagination Specs

Job Specs

Document Security Specs

Export Audit Specs

Update existing tests where necessary.

All tests must pass.

---

# Deliverables

Booking Hardening

CRM Merge Improvements

Availability Migration

Pagination

Async Jobs

Signed Document URLs

Export Audit

Updated Tests

Engineering Review

---

# Acceptance Criteria

✓ Staff availability fully validated

✓ Double booking prevented

✓ CRM merge migrates appointments

✓ working_hours is canonical

✓ Pagination implemented

✓ Imports and exports run asynchronously

✓ Signed document URLs implemented

✓ Export audit created

✓ Tests pass

✓ Rubocop passes

✓ Brakeman passes

Stop after completion.

Generate Engineering Review.

Wait for architect approval.

---

# Completion Report

Populate

98_Engineering_Reviews/Sprint-03/Reviews/HARDENING-001.md

Include

- Summary
- Files Created
- Files Modified
- Database Changes
- API Changes
- Tests Added
- Performance Improvements
- Security Improvements
- Technical Debt Removed
- Remaining Risks

---

# Roadmap Progress

✅ AUTH

✅ BUSINESS

✅ AI Foundation

✅ CRM

✅ BOOKINGS

✅ OPERATIONS

⬜ HARDENING

⬜ COMMUNICATIONS

⬜ AI Runtime

⬜ REPORTS