# ENGINEERING TASK

ID

NOTIFICATIONS-001

Sprint

Sprint 05

Title

Notification Center

Status

Approved

Depends On

AUTO-001

COMMS-001

BOOK-001

CRM-003

AI-007

---

# Objective

Implement a centralized Notification Center.

Every module within Zorovex must publish notifications through one unified service.

Notifications must never be generated directly by individual modules.

---

# Philosophy

Notifications are events.

Modules publish events.

Notification Center decides

- who should receive them
- when they should be delivered
- how they should appear
- whether they should be grouped
- whether they should trigger external delivery

---

# Scope

Implement

- Notification Service
- Notification Preferences
- Notification Feed
- Notification Groups
- Priority System
- Read Status
- Archive
- Notification Templates
- Delivery Channels
- Notification History

---

# Notification Types

Support

Information

Success

Warning

Error

Reminder

Approval Required

Booking

Payment

Conversation

AI

Workflow

Business

System

Security

---

# Sources

Bookings

CRM

Communications

AI Runtime

Workflow Engine

Automation Engine

Calendar

Business Settings

Authentication

Platform

---

# Delivery Channels

Current

In-App

Future

WhatsApp

Push

Email

SMS

Webhook

---

# Priority

Support

Critical

High

Normal

Low

Silent

Priority determines

- ordering
- display
- badge count
- future push behaviour

---

# Features

Unread Count

Mark Read

Mark All Read

Archive

Restore

Delete (soft)

Mute

Snooze

Grouping

Filtering

Search

---

# Notification Preferences

Users configure

- enabled channels
- muted notifications
- quiet hours
- working hours
- priority overrides

---

# Templates

Examples

Booking Confirmed

Booking Cancelled

Payment Waiting

Payment Approved

AI Escalation

Workflow Failed

Business Closed

Staff Assigned

Lead Created

Conversation Waiting

Automation Failed

---

# APIs

GET /api/v1/notifications

GET /api/v1/notifications/unread-count

PATCH /api/v1/notifications/:id

PATCH /api/v1/notifications/read-all

PATCH /api/v1/notifications/preferences

---

# Backend

Create

NotificationService

NotificationDispatcher

NotificationPreferenceService

NotificationTemplateService

NotificationHistoryService

NotificationPolicy

NotificationSerializer

Commands

Queries

Validators

Factories

Specs

---

# Frontend

Create

Notification Center

Notification Bell

Notification Feed

Notification Preferences

Notification Filters

Notification Search

Notification Drawer

---

# Permissions

Every authenticated user

Receives notifications according to role.

Owners may configure organization defaults.

---

# Logging

Log

NotificationCreated

NotificationDelivered

NotificationRead

NotificationArchived

NotificationMuted

NotificationFailed

---

# Testing

Create

Notification Specs

Preference Specs

Template Specs

API Specs

Frontend Specs

All tests must pass.

---

# Deliverables

Notification Center

Notification Preferences

Templates

REST APIs

Tests

Engineering Review

---

# Acceptance Criteria

✓ Notification Center operational

✓ Preferences operational

✓ Grouping operational

✓ Read status operational

✓ APIs operational

✓ Tests pass

✓ Rubocop passes

✓ Brakeman passes

Stop after completion.

Generate Engineering Review.

Wait for architect approval.