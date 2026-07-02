# PATCH

ID

AI-005-PATCH-001

Applies To

AI-005

Title

Workflow Engine Refinements

Status

Approved

---

# Objective

Implement the final refinements to the AI Business Workflow Engine before AI-006.

This patch improves booking accuracy, conversation continuity, and business rule separation.

Do not redesign AI-005.

Do not change the Workflow Engine architecture.

Only implement the improvements described below.

---

# Scope

Implement

- Staff Selection
- Temporary Booking Hold
- Workflow Expiration
- Business Rules Service
- Workflow Summary

No additional features.

---

# 1. Staff Selection

Extend the Booking Workflow.

Current flow

Service

↓

Date

↓

Time

New flow

Service

↓

Preferred Staff (if required)

↓

Date

↓

Time

Business Rules determine whether staff selection is required.

Examples

- Any Staff
- Specific Staff
- AI Recommendation

If staff selection is optional, the workflow must skip this step.

Availability must consider the selected staff member.

---

# 2. Temporary Booking Hold

When availability is confirmed, the selected slot must be temporarily reserved.

Reservation duration

15 minutes

During the reservation

- Other booking requests must not receive the same slot.
- The reservation belongs to the active Workflow Session.

If payment is verified within the reservation window

Create the appointment.

If the reservation expires

Release the slot automatically.

Notify the customer that the reservation has expired.

The customer may restart the booking workflow.

---

# 3. Workflow Expiration

Support automatic expiration.

Examples

Waiting Payment

24 hours

↓

Workflow Expired

Waiting Customer

72 hours

↓

Workflow Expired

Expired workflows

- Release any temporary booking hold.
- Update workflow status.
- Log expiration event.
- Notify customer.
- Notify assigned staff (if applicable).

Implement expiration through a background job.

---

# 4. Business Rules Service

Move all payment-related decisions into a dedicated service.

Create

Workflows::BusinessRulesService

Responsibilities

- Deposit required
- Deposit percentage
- Payment methods
- Manual verification
- Staff selection requirement
- Booking hold duration
- Workflow timeout values

The Booking Workflow must consume this service.

No payment logic should remain hardcoded inside the workflow.

---

# 5. Workflow Summary

When a workflow completes

Automatically generate

- Workflow Summary
- Conversation Summary
- Booking Summary (if applicable)

Store summaries

- Workflow Session
- CRM Timeline
- Conversation Thread

These summaries will be reused by future AI memory features.

---

# Logging

Log

BookingHoldCreated

BookingHoldReleased

WorkflowExpired

WorkflowSummaryGenerated

BusinessRulesLoaded

---

# Backend

Create

Workflows::BusinessRulesService

BookingHoldService

WorkflowExpirationJob

WorkflowSummaryService

Update

BookingWorkflow

WorkflowEngine

BusinessActions

WorkflowSession

WorkflowEvents

---

# Testing

Add

- Staff selection workflow specs
- Booking hold specs
- Expiration job specs
- Business rules specs
- Workflow summary specs

All existing tests must continue to pass.

---

# Deliverables

- Staff Selection
- Temporary Booking Hold
- Workflow Expiration
- Business Rules Service
- Workflow Summary
- Tests
- Engineering Review

---

# Acceptance Criteria

✓ Staff selection supported

✓ Temporary booking hold implemented

✓ Booking hold released on timeout

✓ Workflow expiration implemented

✓ Business Rules Service implemented

✓ Workflow summaries generated

✓ Tests pass

✓ RuboCop passes

✓ Brakeman passes

Stop after completion.

Generate Engineering Review.

Do not begin AI-006.