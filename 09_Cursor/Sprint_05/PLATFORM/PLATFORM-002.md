# ENGINEERING TASK

ID

PLATFORM-002

Sprint

Sprint 05

Title

Domain Event Platform

Status

Approved

Depends On

PLATFORM-001

BOOK-001

CRM-003

COMMS-001

AI-005

---

# Objective

Implement the internal Domain Event Platform.

The Domain Event Platform provides a centralized event bus that allows all modules inside Zorovex to communicate without directly depending on one another.

Modules publish events.

Modules subscribe to events.

No module should call another module simply to trigger secondary actions.

---

# Philosophy

Business logic belongs to domain services.

Cross-cutting functionality belongs to subscribers.

Example

Appointment Created

↓

Publish Event

↓

Automation

↓

Notifications

↓

Business Intelligence

↓

Audit

↓

Future Webhooks

No direct coupling.

---

# Scope

Implement

- Domain Event Bus
- Event Publisher
- Event Subscribers
- Event Registry
- Event Dispatcher
- Event Replay
- Dead Letter Queue
- Event Monitoring
- Event Logging

---

# Architecture

Business Module

↓

Publish Domain Event

↓

Event Bus

↓

Subscribers

↓

Actions

---

# Supported Modules

Bookings

CRM

Communications

AI Runtime

Workflow Engine

Automation Engine

Notifications

Business Intelligence

Audit

Calendar

Settings

Future Inventory

Future Marketing

---

# Core Components

Create

DomainEvent

DomainEventBus

DomainEventPublisher

DomainEventSubscriber

DomainEventDispatcher

DomainEventRegistry

EventMonitor

DeadLetterQueue

EventReplayService

---

# Event Lifecycle

Business Action

↓

Domain Event

↓

Validation

↓

Queue

↓

Dispatch

↓

Subscribers

↓

Completion

↓

Archive

---

# Event Structure

Every event must contain

Event ID

Event Name

Version

Organization ID

Entity Type

Entity ID

Actor Type

Actor ID

Occurred At

Correlation ID

Request ID

Payload

Metadata

---

# Event Categories

Booking

CRM

Conversation

AI

Workflow

Automation

Notification

Payment

Calendar

Security

Settings

Platform

System

---

# Standard Events

AppointmentCreated

AppointmentUpdated

AppointmentCancelled

AppointmentCompleted

ConversationStarted

ConversationClosed

LeadCreated

CustomerCreated

WorkflowStarted

WorkflowCompleted

WorkflowCancelled

NotificationCreated

PaymentRequested

PaymentVerified

BusinessSettingsUpdated

UserLoggedIn

RoleChanged

Future modules must follow the same convention.

---

# Subscribers

Examples

Automation Engine

AppointmentCreated

↓

Appointment Reminder

Notification Center

WorkflowCompleted

↓

Owner Notification

Business Intelligence

ConversationClosed

↓

Update KPIs

Audit Platform

Every Event

↓

Audit Entry

---

# Ordering

Support

Sequential

Parallel

Priority

Retry

---

# Failure Handling

If subscriber fails

Retry

↓

Retry Limit

↓

Dead Letter Queue

↓

Administrator Notification

Publishing module must never fail because a subscriber failed.

---

# Event Replay

Support replay

Single Event

Date Range

Organization

Entity

Subscriber

Replay must never create duplicate business data.

Subscribers must be idempotent.

---

# Monitoring

Track

Events Published

Events Processed

Events Failed

Retry Count

Subscriber Latency

Queue Size

Dead Letter Count

---

# APIs

GET /api/v1/platform/events

GET /api/v1/platform/events/:id

GET /api/v1/platform/events/failed

POST /api/v1/platform/events/replay

---

# Backend

Create

DomainEvent

DomainEventBus

DomainEventDispatcher

SubscriberRegistry

PublisherService

ReplayService

DeadLetterQueue

MonitoringService

Policies

Commands

Queries

Serializers

Validators

Factories

Specs

---

# Frontend

Create

Event Monitor

Subscriber Monitor

Dead Letter Queue

Replay Panel

Event Explorer

---

# Permissions

Owner

Full

Manager

Read

System Admin

Replay

Developers (future)

Diagnostics

---

# Logging

Log

EventPublished

EventProcessed

EventFailed

EventRetried

ReplayStarted

ReplayCompleted

DeadLetterCreated

---

# Testing

Create

Publisher Specs

Subscriber Specs

Dispatcher Specs

Replay Specs

Dead Letter Specs

API Specs

Frontend Specs

All tests must pass.

---

# Deliverables

Domain Event Platform

Publisher

Subscriber Framework

Replay

Monitoring

Dead Letter Queue

REST APIs

Tests

Engineering Review

---

# Acceptance Criteria

✓ Event Bus operational

✓ Subscribers operational

✓ Retry operational

✓ Dead Letter Queue operational

✓ Replay operational

✓ Monitoring operational

✓ APIs operational

✓ Tests pass

✓ RuboCop passes

✓ Brakeman passes

Stop after completion.

Generate Engineering Review.

Wait for architect approval.

---

# Completion Report

Populate

98_Engineering_Reviews/Sprint-05/Reviews/PLATFORM-002.md

Include

- Summary
- Files Created
- Files Modified
- Event Definitions
- Subscribers
- Replay
- Monitoring
- APIs
- Tests Added
- Assumptions
- Risks
- Technical Debt