# AUTO-001 — Engineering Review

**Task:** AUTO-001 (Automation Engine)
**Sprint:** Sprint 05
**Status:** Pending Architect Approval
**Depends On:** CRM-003, BOOK-001, COMMS-001, AI-007, BI-001

---

## Summary

Implemented the centralized Automation Engine. Business modules publish events through `Automations::EventPublisher`; the engine matches active rules, evaluates conditions, executes actions, supports delayed execution, and records execution history. APIs expose rule management, templates, history, and test execution at `/api/v1/automations`. Frontend dashboard is available at `/automations`.

---

## Services Added

| Service | Purpose |
|---------|---------|
| `Automations::EventBus` | Central event ingress for automation processing |
| `Automations::EventPublisher` | Module-facing publisher for bookings, CRM, comms, workflows |
| `Automations::AutomationEngine` | Orchestrates trigger matching and rule execution |
| `Automations::TriggerEngine` | Finds active rules for an event type |
| `Automations::ConditionEngine` | Evaluates rule conditions against event payload |
| `Automations::ActionEngine` | Executes notifications, CRM activities, tasks, assignments, workflows |
| `Automations::AutomationRunner` | Creates execution records, handles retries |
| `Automations::DelayQueue` | Schedules delayed action continuation |
| `Automations::TemplateService` | Built-in automation templates |
| `Automations::HistoryService` | Execution history listing |
| `Automations::EventLogger` | Structured automation audit logging |

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/v1/automations` | List active automation rules |
| POST | `/api/v1/automations` | Create automation rule |
| PATCH | `/api/v1/automations/:id` | Update automation rule |
| DELETE | `/api/v1/automations/:id` | Archive automation rule |
| GET | `/api/v1/automations/templates` | List built-in templates |
| GET | `/api/v1/automations/history` | Execution history |
| POST | `/api/v1/automations/test` | Test rule against sample event |

---

## Event Integrations

| Module | Events Published |
|--------|------------------|
| Bookings | `appointment_created`, `appointment_updated`, `appointment_cancelled`, `appointment_completed` |
| CRM | `lead_created` / `customer_created` on contact create |
| Communications | `conversation_started`, `conversation_closed` |
| Workflows | `workflow_failed` on session expiration |

---

## Frontend

| Route | Feature |
|-------|---------|
| `/automations` | Rules list, templates, history, test runner |

Access is role-gated via `AutomationPolicy` (view: owner/manager/receptionist/marketing/accountant; manage: owner/manager/marketing/accountant).

---

## Database

| Table | Purpose |
|-------|---------|
| `automation_rules` | Rule definitions |
| `automation_executions` | Execution log |
| `automation_delay_jobs` | Delayed action queue |

---

## Tests

- `spec/requests/automations_spec.rb`
- `spec/services/automations/condition_engine_spec.rb`
- `spec/services/automations/automation_engine_spec.rb`

---

## Notes / Follow-ups

- Feature gated to `professional`+ plans via `Platform::FeatureAccessService`
- Additional action types (WhatsApp, booking mutations) are scaffolded but not fully implemented
- AI escalation publisher hook pending AI runtime integration
- Customer update events not yet wired on CRM update command
