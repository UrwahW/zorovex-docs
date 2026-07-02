# PLATFORM-002 — Engineering Review

**Task:** PLATFORM-002 (Domain Event Platform)
**Sprint:** Sprint 05
**Status:** Pending Architect Approval
**Depends On:** PLATFORM-001, BOOK-001, CRM-003, COMMS-001, AI-005

---

## Summary

Implemented the internal Domain Event Platform. Modules publish domain events through `Platform::DomainEvents::PublisherService`; the bus dispatches asynchronously to registered subscribers with retries, dead-letter handling, monitoring, and replay. `Automations::EventBus` now routes through the domain event platform. Subscribers include Automations and Audit.

---

## Services Added

| Service | Purpose |
|---------|---------|
| `Platform::DomainEvents::PublisherService` | Validate and persist domain events |
| `Platform::DomainEvents::DomainEventBus` | Public publish API |
| `Platform::DomainEvents::DomainEventDispatcher` | Subscriber dispatch with retry |
| `Platform::DomainEvents::SubscriberRegistry` | Subscriber registration |
| `Platform::DomainEvents::DeadLetterQueue` | Failed delivery storage |
| `Platform::DomainEvents::ReplayService` | Event and scope replay |
| `Platform::DomainEvents::MonitoringService` | Metrics and event listing |
| `Platform::DomainEvents::DispatchJob` | Async dispatch worker |

---

## Subscribers

| Subscriber | Behavior |
|------------|----------|
| `automations` | Routes to `Automations::AutomationEngine` |
| `audit` | Routes to `Audit::AuditEventService` |

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/v1/platform/events` | Event explorer + monitoring snapshot |
| GET | `/api/v1/platform/events/:id` | Event detail with deliveries |
| GET | `/api/v1/platform/events/failed` | Dead letter queue |
| POST | `/api/v1/platform/events/replay` | Replay event or scope |

---

## Frontend

| Route | Feature |
|-------|---------|
| `/platform/events` | Event monitor, dead letter queue, replay controls |

---

## Database

| Table | Purpose |
|-------|---------|
| `domain_events` | Published events |
| `domain_event_deliveries` | Per-subscriber delivery status |
| `domain_event_dead_letters` | Failed deliveries after retries |

---

## Tests

- `spec/requests/platform_events_spec.rb`
- `spec/services/platform/domain_events/publisher_service_spec.rb`
- `spec/services/platform/domain_events/domain_event_dispatcher_spec.rb`

---

## Notes / Follow-ups

- BI and Notification subscribers can be added to `SubscriberRegistry` in a follow-up
- Publishing modules never fail when subscribers fail (errors captured per delivery)
- Replay is idempotent for successful deliveries
