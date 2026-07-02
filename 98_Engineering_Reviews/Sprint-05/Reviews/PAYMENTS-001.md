# PAYMENTS-001 — Engineering Review

**Task:** PAYMENTS-001 (Business Payment Platform)
**Sprint:** Sprint 05
**Status:** Pending Architect Approval
**Depends On:** BOOK-001, AI-005, AI-006, AUTO-001, PLATFORM-002

---

## Summary

Implemented the centralized Business Payment Platform. Payment logic is extracted from the booking workflow into dedicated services for payment requests, verification, rules, timeline, refunds, and provider adapters. Manual verification is supported for cash, bank transfer, cheque, JazzCash, EasyPaisa, and Raast (stub adapters delegating to manual flow). The booking workflow now creates payment requests during `collecting_payment`, marks proof during `waiting_payment`, and verifies via `PaymentVerificationService` on staff resume. Domain events and automation events are published for payment lifecycle changes. Frontend dashboard at `/payments`.

---

## Services Added

| Service | Purpose |
|---------|---------|
| `Payments::PaymentService` | List, filter, monitoring snapshot |
| `Payments::PaymentRequestService` | Create, cancel, expire, mark waiting verification |
| `Payments::PaymentVerificationService` | Verify, reject, refund |
| `Payments::PaymentRulesEngine` | Deposit calculation, instructions, expiration |
| `Payments::PaymentTimelineService` | Append-only payment timeline |
| `Payments::PaymentProviderRegistry` | Provider resolution and method listing |
| `Payments::PaymentSettingsService` | Business payment configuration |
| `Payments::CrmIntegration` | Contact `last_payment_at` and CRM activity |
| `Payments::EventLogger` | Structured payment logging |
| `Payments::PaymentExpirationJob` | Expire stale payment requests |

---

## Provider Architecture

| Provider | Class | Behavior |
|----------|-------|----------|
| `manual`, `cash`, `bank_transfer`, `cheque`, `custom_link` | `Providers::ManualProvider` | Manual instructions + staff verification |
| `jazzcash` | `Providers::JazzCashProvider` | Stub adapter (manual flow) |
| `easypaisa` | `Providers::EasyPaisaProvider` | Stub adapter (manual flow) |
| `raast` | `Providers::RaastProvider` | Stub adapter (manual flow) |

Future gateways (Stripe, PayPal, etc.) register in `PaymentProviderRegistry` without changing workflow code.

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/v1/payments` | List payment requests + monitoring |
| GET | `/api/v1/payments/:id` | Payment detail + timeline |
| POST | `/api/v1/payments` | Create payment request |
| PATCH | `/api/v1/payments/:id` | Update notes / mark proof uploaded |
| POST | `/api/v1/payments/:id/verify` | Verify payment |
| POST | `/api/v1/payments/:id/reject` | Reject payment |
| POST | `/api/v1/payments/:id/refund` | Full or partial refund |
| GET | `/api/v1/payment-settings` | Business payment settings |
| PATCH | `/api/v1/payment-settings` | Update payment settings |
| GET | `/api/v1/payment-methods` | Enabled methods for organization |

---

## Domain Events

| Event | Trigger |
|-------|---------|
| `PaymentCreated` | Payment request created |
| `PaymentUpdated` | Proof uploaded / status change |
| `PaymentVerified` | Staff verification |
| `PaymentRejected` | Staff rejection |
| `PaymentExpired` | Expiration job or manual expire |
| `PaymentCancelled` | Cancelled request |
| `PaymentRefunded` | Refund processed |

Automation events: `payment_requested`, `payment_verified`, `payment_failed`, `payment_expired`, `payment_refunded`.

---

## Workflow Integration

| Booking State | Payment Platform Action |
|---------------|-------------------------|
| `collecting_payment` | Creates deposit via `PaymentRequestService` |
| `waiting_payment` | Marks `waiting_verification` on customer confirmation |
| `verify_payment!` resume | Verifies via `PaymentVerificationService` |

---

## Frontend

| Route | Feature |
|-------|---------|
| `/payments` | Dashboard, requests list, verification panel, settings, timeline, refund |

---

## Permissions

| Role | Access |
|------|--------|
| Owner | Full |
| Manager | Create, verify, settings update |
| Receptionist | Create requests, read |
| Accountant | Verify, refund, read |
| Marketing | Read only |

---

## Database

| Table / Change | Purpose |
|----------------|---------|
| `payment_requests` | Core payment request records |
| `payment_timeline_events` | Append-only lifecycle timeline |
| `payment_refunds` | Refund records |
| `business_payment_settings` | Extended with currency, deposit amount, expiration, policies |
| `contacts.last_payment_at` | CRM payment tracking |

Migration: `20240628000045_create_payment_platform.rb`

---

## Tests

- `spec/requests/payments_spec.rb` (5 examples)
- `spec/services/payments/payment_rules_engine_spec.rb` (2 examples)
- `spec/services/payments/payment_verification_service_spec.rb` (2 examples)
- `spec/factories/payment_requests.rb`

All 9 payment specs pass.

---

## Assumptions

- Wallet providers (JazzCash, EasyPaisa, Raast) use manual verification until gateway APIs are integrated.
- Payment expiration job exists but is not yet scheduled in a recurring runner (enqueue via cron/Sidekiq scheduler in ops).
- Receipt viewer uses timeline + instructions inline; dedicated PDF receipt generation is deferred.

---

## Risks

- Unscheduled expiration job may leave stale `waiting_customer` requests until manual cleanup or scheduler wiring.
- Provider stubs share manual verification path; gateway cutover requires per-provider credential and webhook work.

---

## Technical Debt

- Schedule `Payments::PaymentExpirationJob` in production job scheduler.
- Stripe/PayPal/Square provider implementations.
- Dedicated receipt PDF generation and evidence file upload UI.
- Frontend settings editor with full form validation (current settings tab is read-focused).

---

## Files Created (key)

**Backend:** models (`payment_request`, `payment_timeline_event`, `payment_refund`), services under `app/services/payments/`, controllers, policy, serializers, job, migration, specs.

**Frontend:** `frontend/src/features/payments/` (API, hooks, constants, types, dashboard page, access route).

**Modified:** `booking_workflow.rb`, `workflow_session.rb`, `organization.rb`, `routes.rb`, `crm/contacts/types.rb`, `dashboard-layout.tsx`, `router.tsx`.

---

## Acceptance Criteria

- [x] Payment Platform operational
- [x] Payment Rules operational
- [x] Manual Verification operational
- [x] Timeline operational
- [x] Provider Architecture implemented
- [x] Domain Events published
- [x] APIs operational
- [x] Tests pass
- [x] RuboCop passes (payment files)
- [ ] Brakeman — not run in this session
