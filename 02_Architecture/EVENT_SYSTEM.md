# Event System

---

# Philosophy

Domains should communicate using events whenever possible.

Events reduce coupling.

Consumers should not know who emitted the event.

---

# Event Categories

Platform Events

Business Events

Communication Events

Booking Events

Catalog Events

AI Events

Automation Events

Notification Events

---

# Flow

Action

↓

Domain Service

↓

Event

↓

Subscribers

↓

Side Effects

---

# Example

Catalog Published

↓

BusinessReadiness

↓

AI Knowledge Refresh

↓

Search Index

↓

Analytics

↓

Notifications

No direct coupling.

---

# Event Naming

Past tense.

Examples

BookingCreated

BookingCancelled

CatalogPublished

PromotionActivated

ConversationAssigned

AiExecutionCompleted

CustomerCreated

CustomerMerged

OrganizationProvisioned

SupportSessionStarted

---

# Event Metadata

Every event contains

id

organization_id

actor_id

occurred_at

correlation_id

payload

version

---

# Correlation IDs

Every request has

Request ID

Correlation ID

Execution ID

These travel through

API

Jobs

Events

AI Runtime

Logging

---

# Event Delivery

Synchronous

Used only when immediate consistency required.

Asynchronous

Preferred.

Background jobs consume events.

---

# AI Events

IntentResolved

WorkflowExecuted

ProviderExecuted

ValidationFailed

HumanHandoffTriggered

GuardrailTriggered

ExecutionCompleted

---

# Catalog Events

ServiceCreated

PromotionPublished

PricingChanged

HolidayCreated

CatalogPublished

ImportCompleted

ExtractionCompleted

---

# Platform Events

OrganizationCreated

SubscriptionChanged

FeatureOverrideUpdated

SupportSessionStarted

SupportSessionEnded

---

# Event Consumers

Automation

Notifications

Analytics

AI Runtime

Search

Platform Dashboard

Audit

---

# Rules

Events never mutate state directly.

Events describe something that already happened.

Commands change state.

Events report state.

---

Future

Event Bus

Kafka

Outbox Pattern

Replay

Dead Letter Queue