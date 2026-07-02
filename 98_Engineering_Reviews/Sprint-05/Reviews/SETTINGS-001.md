# SETTINGS-001 — Engineering Review

**Task:** SETTINGS-001 (Business Configuration Platform)
**Sprint:** Sprint 05
**Status:** Pending Architect Approval
**Depends On:** CORE-001, PAYMENTS-001, CALENDAR-001, AUTO-001, AI-007

**Note:** UI-001 (Sprint 06 UX) was intentionally **not** implemented.

---

## Summary

Implemented the Business Configuration Platform as the centralized operational rules layer. A unified `/api/v1/settings` API aggregates working hours, booking rules, cancellation rules, payment defaults, AI defaults, communication defaults, staff defaults, automation defaults, service defaults, and business policies. Configuration delegates to existing models (`BusinessPaymentSetting`, `BusinessAiReceptionistSetting`, `working_hours`, `business_channels`) while storing module-specific JSON rules in `business_configurations`. Templates support export, import, clone, and reset. Frontend dashboard at `/settings`. RBAC `settings.view` / `settings.update` permissions are now wired.

---

## Configuration Areas

| Area | Source |
|------|--------|
| Working Hours | Operations `working_hours` + calendar holidays + blackout dates |
| Booking Rules | `business_configurations.booking_rules` + `business_payment_setting` timeouts |
| Cancellation Rules | `business_configurations.cancellation_rules` + payment refund policies |
| Payment Defaults | `business_payment_setting` via `PaymentDefaultsService` |
| AI Defaults | `business_ai_receptionist_setting` + `ai_defaults` JSON |
| Communication Defaults | `business_channels` + `communication_defaults` JSON |
| Staff Defaults | `staff_defaults` JSON + staff selection mode |
| Automation Defaults | `automation_defaults` JSON |
| Service Defaults | `service_defaults` JSON |
| Business Policies | `business_policies` JSON (blackout dates, emergency closures) |

---

## Services Added

| Service | Purpose |
|---------|---------|
| `Settings::BusinessConfigurationService` | Aggregate show/update |
| `Settings::WorkingHoursService` | Hours, holidays, blackouts |
| `Settings::BookingRulesService` | Booking operational rules |
| `Settings::PaymentDefaultsService` | Payment configuration facade |
| `Settings::AiDefaultsService` | AI receptionist defaults |
| `Settings::CommunicationDefaultsService` | Channel + comms defaults |
| `Settings::AutomationDefaultsService` | Automation policy defaults |
| `Settings::StaffDefaultsService` | Staff assignment defaults |
| `Settings::ServiceDefaultsService` | Service timing defaults |
| `Settings::ConfigurationTemplateService` | Export/import/clone/reset/templates |

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/v1/settings` | Full business configuration |
| PATCH | `/api/v1/settings` | Update configuration sections |
| GET | `/api/v1/settings/templates` | System + custom templates |
| GET | `/api/v1/settings/export` | Export JSON configuration |
| POST | `/api/v1/settings/import` | Import JSON configuration |

---

## Domain Events

| Event | Trigger |
|-------|---------|
| `SettingsUpdated` | Any configuration patch |
| `WorkingHoursUpdated` | Working hours change |
| `BookingRulesUpdated` | Booking rules change |
| `AiDefaultsUpdated` | AI defaults change |
| `CommunicationDefaultsUpdated` | Communication defaults change |
| `AutomationDefaultsUpdated` | Automation defaults change |

---

## Database

| Table | Purpose |
|-------|---------|
| `business_configurations` | JSON sections per organization |
| `business_configuration_templates` | Saved/importable templates |

Migration: `20240628000048_create_business_configuration_platform.rb`

---

## Frontend

| Route | Feature |
|-------|---------|
| `/settings` | Business settings dashboard with tabs for hours, booking, payments, AI, communication, automation, templates |

---

## Permissions

Uses `settings.view` / `settings.update` RBAC permissions with role fallback (owner/manager for update).

---

## Tests

- `spec/requests/settings_spec.rb` (4 examples)
- `spec/services/settings/configuration_template_service_spec.rb` (1 example)

All 5 settings specs pass.

---

## Assumptions

- Operational rules remain in existing tables where already mature; `business_configurations` holds defaults and cross-module JSON.
- Payment settings API remains available; settings platform includes payment defaults in aggregate.
- UI-001 global UX polish is out of scope.

---

## Risks

- Dual edit paths (e.g. `/payments` settings tab vs `/settings`) until UX consolidation.
- Not all modules yet read from `business_configurations` JSON at runtime — some still read legacy tables only.

---

## Technical Debt

- Wire booking/AI modules to read `business_configurations` booking_rules at runtime (beyond payment setting fields).
- Full settings form editors per section (current UI is read-focused with limited save).
- UI-001 Sprint 06 UX pass (deferred — requires separate approval).

---

## Acceptance Criteria

- [x] Business Configuration operational
- [x] Working Hours operational
- [x] Booking Rules operational
- [x] AI Defaults operational
- [x] Configuration Templates operational
- [x] APIs operational
- [x] Tests pass
- [ ] RuboCop / Brakeman — not run full suite in this session
