# ENGINEERING TASK

ID

COMMS-001

Sprint

Sprint 3

Title

Communications Platform

Status

Approved

Depends On

OPS-001

---

# Objective

Implement the Communications Platform.

This module centralizes every customer communication inside Zorovex.

All future communication providers will use this module.

This PR creates the communication layer.

Provider integrations come later.

---

# Scope

Implement

- Unified Inbox
- Conversation Threads
- Messages
- Templates
- Internal Notes
- Channels
- Attachments
- Message Timeline
- Contact Communication History
- Notifications

---

# Database

Create

communication_threads

messages

message_templates

message_attachments

notifications

---

# Communication Thread

Columns

id

organization_id

contact_id

channel

status

last_message_at

assigned_to

created_at

updated_at

---

# Message

Columns

id

thread_id

sender_type

direction

message_type

content

status

provider_reference

metadata

created_at

updated_at

deleted_at

---

# Channels

Allowed

whatsapp

email

sms

instagram

facebook

website_chat

internal

---

# Direction

incoming

outgoing

internal

---

# Message Status

draft

queued

sent

delivered

read

failed

---

# Templates

Support

- Variables
- Categories
- Preview
- Duplicate
- Archive

Variables use

{{customer_name}}

{{service_name}}

{{appointment_date}}

etc.

---

# Notifications

Support

Appointment Reminder

Booking Cancelled

Task Assigned

System Alert

New Message

No provider delivery.

Store notifications only.

---

# Unified Inbox

Display

Conversation List

Conversation View

Customer Profile

Attachments

Timeline

Notes

Upcoming Appointment

Recent Activity

---

# Backend

Create

CommunicationThread

Message

MessageTemplate

Notification

Policies

Commands

Queries

Validators

Serializers

Factories

REST Controllers

Services

TemplateEngine

NotificationService

ConversationService

---

# API

GET

/api/v1/comms/threads

GET

/api/v1/comms/threads/:id

POST

/api/v1/comms/messages

PATCH

/api/v1/comms/messages/:id

GET

/api/v1/comms/templates

POST

/api/v1/comms/templates

PATCH

/api/v1/comms/templates/:id

DELETE

/api/v1/comms/templates/:id

GET

/api/v1/comms/notifications

PATCH

/api/v1/comms/notifications/:id

---

# Frontend

Create

Inbox

Conversation

Message Composer

Template Manager

Notification Center

Conversation Sidebar

Attachment Viewer

Message Search

Filters

---

# Inbox

Support

Unread

Assigned

Archived

Resolved

Search

Filter by Channel

Filter by Customer

---

# Contact Integration

Each CRM Contact displays

Messages

Threads

Notifications

Timeline

Attachments

---

# Booking Integration

Appointments display

Communication History

Reminder Status

Related Messages

---

# Permissions

Owner

Full Access

Manager

Full Access

Receptionist

Read

Create

Reply

Marketing

Templates

Read

Accountant

Read

---

# Logging

ThreadCreated

MessageCreated

MessageUpdated

TemplateCreated

NotificationCreated

---

# Events

MessageCreated

ThreadCreated

NotificationCreated

---

# Out of Scope

WhatsApp Cloud API

Meta API

Twilio

SMTP

Instagram Graph API

Facebook Messenger API

AI Replies

Voice Calls

Push Notifications

---

# Testing

Create

Model Specs

Request Specs

Policy Specs

Service Specs

Template Specs

Notification Specs

Frontend Tests

Routing Tests

All tests must pass.

---

# Deliverables

Unified Inbox

Conversation Threads

Templates

Notifications

REST API

Tests

Engineering Review

---

# Acceptance Criteria

✓ Inbox operational

✓ Conversations operational

✓ Templates operational

✓ Notifications operational

✓ CRM integration working

✓ Booking integration working

✓ Tests pass

✓ Rubocop passes

✓ Brakeman passes

Stop after completion.

Generate Engineering Review.

Wait for architect approval.

---

# Completion Report

Populate

98_Engineering_Reviews/Sprint-03/Reviews/COMMS-001.md

Include

- Summary
- Files Created
- Files Modified
- Database Changes
- API Endpoints
- Tests Added
- Assumptions
- Risks
- Technical Debt

---

# Roadmap Progress

✅ AUTH

✅ BUSINESS

✅ AI Foundation

✅ CRM

✅ BOOKINGS

✅ OPERATIONS

⬜ COMMUNICATIONS

⬜ AI Runtime

⬜ REPORTS