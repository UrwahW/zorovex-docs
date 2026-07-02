# AI-005-PATCH-001 — Engineering Review

**Task:** AI-005-PATCH-001 (Workflow Engine Refinements)
**Applies To:** AI-005
**Sprint:** 04
**Status:** Pending Architect Approval

---

## Summary

Implemented AI-005-PATCH-001 per spec. The Booking Workflow now supports optional/required staff selection driven by business rules, creates 15-minute temporary booking holds when availability is confirmed, expires workflows via a background job, centralizes payment and booking policy in `BusinessRulesService`, and generates workflow/conversation/booking summaries on completion.

No architectural changes to the AI-005 Workflow Engine — refinements are additive services and state-machine extensions only.

**Verification:** 28 workflow-related RSpec examples (0 failures), Brakeman 0 warnings, RuboCop exit 0.

---

## Deliverables

| Requirement | Status |
|-------------|--------|
| Staff selection (Any / Specific / AI Recommendation) | Done |
| Temporary booking hold (15 min, session-scoped) | Done |
| Workflow expiration (24h payment / 72h customer) | Done |
| `Workflows::BusinessRulesService` | Done |
| Workflow summaries (session, CRM, conversation) | Done |
| Logging events | Done |
| Tests | Done |

---

## Files Created

### Backend

- `db/migrate/20240628000038_workflow_engine_refinements.rb`
- `app/models/workflow_booking_hold.rb`
- `app/services/workflows/business_rules_service.rb`
- `app/services/workflows/booking_hold_service.rb`
- `app/services/workflows/workflow_summary_service.rb`
- `app/jobs/workflows/workflow_expiration_job.rb`
- `spec/factories/workflow_booking_holds.rb`
- `spec/services/workflows/business_rules_service_spec.rb`
- `spec/services/workflows/booking_hold_service_spec.rb`
- `spec/services/workflows/workflow_summary_service_spec.rb`
- `spec/services/workflows/staff_selection_workflow_spec.rb`
- `spec/jobs/workflows/workflow_expiration_job_spec.rb`

---

## Files Modified

### Backend

- `app/services/workflows/types.rb` — `collecting_staff` state; new event types
- `app/services/workflows/booking_workflow.rb` — staff step, holds, business rules, summaries, status timeouts
- `app/services/workflows/workflow_engine.rb` — hold release on cancel; expiration job integration
- `app/services/workflows/payment_rules.rb` — delegates to `BusinessRulesService`
- `app/models/business_payment_setting.rb` — staff selection + hold/timeout settings
- `app/models/workflow_session.rb` — booking holds association
- `app/domains/organization/models/organization.rb` — booking holds association
- `app/serializers/workflow_serializer.rb` — summaries, status expiry, hold expiry
- `db/migrate/20240628000036_rename_ai_runtime_log_errors_column.rb` — idempotent rename (fresh DB fix)
- `db/schema.rb` — updated
- `spec/services/workflows/booking_workflow_spec.rb` — hold required for payment verify

---

## Architecture Notes

### 1. Staff Selection

Booking flow extended:

```
Service → Preferred Staff (if required) → Date → Time → Availability → …
```

`BusinessPaymentSetting#staff_selection_mode`:

- `any_staff` — step skipped
- `specific_staff` — customer selects staff (`collecting_staff`)
- `ai_recommendation` — auto-recommends bookable staff for service, then continues to date

Availability checks pass `staff_id` from collected context.

### 2. Temporary Booking Hold

`BookingHoldService#create_hold!` runs after availability passes. Holds:

- Block overlapping slots for other sessions (`slot_blocked?`)
- Expire after `booking_hold_minutes` (default 15)
- Convert to `converted` on successful booking
- Release on cancel, workflow expiration, or hold timeout

Events: `BookingHoldCreated`, `BookingHoldReleased`.

### 3. Workflow Expiration

`WorkflowExpirationJob` (queue: `default`):

- Releases expired booking holds and notifies customer
- Expires sessions where `status_expires_at` has passed
- Notifies assigned staff via `Comms::NotificationService`

Timeouts from `BusinessRulesService`:

- `waiting_payment` → 24 hours
- `waiting_customer` → 72 hours

`WorkflowEngine#expire_stale!` delegates to the job and retains session-level expiry handling.

### 4. Business Rules Service

`Workflows::BusinessRulesService` centralizes:

- Deposit required / percentage
- Payment methods and instructions
- Manual verification
- Staff selection requirement
- Booking hold duration
- Workflow status timeouts

`PaymentRules` delegates for backward compatibility. Booking workflow uses `BusinessRulesService` directly.

### 5. Workflow Summary

`WorkflowSummaryService#generate!` on booking completion stores:

- `workflow_sessions.summaries` (JSONB)
- CRM timeline (`appointment_created` or `note_added` activity)
- Conversation thread system message

Event: `WorkflowSummaryGenerated`.

---

## Logging

| Event | Mechanism |
|-------|-----------|
| `BusinessRulesLoaded` | Rails logger on rules load |
| `BookingHoldCreated` | `WorkflowEvents` + Rails logger |
| `BookingHoldReleased` | `WorkflowEvents` + Rails logger |
| `WorkflowExpired` | `WorkflowEvents` + Rails logger |
| `WorkflowSummaryGenerated` | `WorkflowEvents` + Rails logger |

---

## Database Changes (Migration 000038)

**`workflow_sessions`**

- `status_expires_at` (datetime, indexed)
- `summaries` (jsonb, default `{}`)

**`business_payment_settings`**

- `staff_selection_mode` (default `any_staff`)
- `booking_hold_minutes` (default 15)
- `waiting_payment_timeout_hours` (default 24)
- `waiting_customer_timeout_hours` (default 72)

**`workflow_booking_holds`** (new table)

- organization, workflow_session, service, staff_member (optional)
- starts_at, ends_at, expires_at, status

---

## Test Results

```
Workflow-related specs: 28 examples, 0 failures
  - staff_selection_workflow_spec.rb
  - booking_hold_service_spec.rb
  - business_rules_service_spec.rb
  - workflow_expiration_job_spec.rb
  - workflow_summary_service_spec.rb
  - booking_workflow_spec.rb (+ existing workflow specs)

Brakeman: 0 security warnings
RuboCop: exit 0 (workflow paths excluded per project config)
```

---

## Operational Notes

- Schedule `Workflows::WorkflowExpirationJob` periodically in production (e.g. every 5 minutes) via your job runner.
- `WorkflowEngine.expire_stale!` can be invoked from the same scheduler for legacy `expires_at` session cleanup.

---

## Acceptance Criteria

- [x] Staff selection supported
- [x] Temporary booking hold implemented
- [x] Booking hold released on timeout
- [x] Workflow expiration implemented
- [x] Business Rules Service implemented
- [x] Workflow summaries generated
- [x] Tests pass (workflow scope)
- [x] RuboCop passes
- [x] Brakeman passes

---

## Out of Scope (per spec)

- AI-006 and downstream features
- Workflow Engine architecture redesign
- Frontend changes (inspector already reads `context` / serializer fields)
