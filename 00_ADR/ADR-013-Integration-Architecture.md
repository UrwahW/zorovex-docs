# Architecture Decision Record

# ADR-013 — Integration Architecture

Status

Accepted

Date

2026-06-30

Owner

Chief Architect

Related

PATCH-001

AI-006

COMMS-001

PLATFORM-002

---

# Context

Zorovex communicates with customers through multiple external providers.

Examples

- WhatsApp
- Instagram
- Facebook Messenger
- Website Chat
- Future Voice
- Future Telegram
- Future Email

Every provider has different

- APIs
- Webhooks
- Authentication
- Message formats
- Retry behaviour

Business logic must never depend on provider-specific payloads.

---

# Decision

Every external provider shall communicate with Zorovex through a Provider Adapter.

Business modules must only consume Canonical Events.

No module may directly parse provider payloads.

---

# Integration Architecture

External Provider

↓

Provider Adapter

↓

Verification

↓

Normalization

↓

Canonical Event

↓

Platform Event Bus

↓

Comms

↓

AI Runtime

↓

CRM

↓

Bookings

↓

Automation

↓

Business Intelligence

---

# Responsibilities

## Provider

Responsible for

- Authentication
- Webhooks
- Retry delivery
- Rate limits

---

## Provider Adapter

Responsible for

- Verification
- Signature validation
- Authentication
- Payload parsing
- Media extraction
- Canonical mapping
- Retry handling
- Idempotency

Nothing else.

---

## Canonical Event

Represents

One business event.

Never provider specific.

Example

CustomerMessageReceived

CustomerMessageDelivered

CustomerMessageRead

CustomerTyping

CallStarted

CallEnded

CustomerReactionAdded

MessageDeleted

AttachmentUploaded

---

# Canonical Message

Every provider becomes

```
Customer Message
```

Regardless of source.

Required fields

Organization ID

Provider

Channel

Conversation ID

Customer ID

External Message ID

Timestamp

Direction

Message Type

Text

Media

Metadata

Raw Payload

---

# Supported Channels

Current

WhatsApp

Instagram

Facebook

Website Chat

Future

Voice

Telegram

Email

SMS

Slack

Microsoft Teams

---

# Provider Registry

Every provider registers itself.

Interface

Provider Name

Version

Capabilities

Webhook Routes

Supported Events

Authentication

Health Status

---

# Provider Capabilities

Examples

Supports

Typing Indicator

Read Receipts

Media

Voice

Location

Buttons

Templates

Business Profile

Capabilities must never be assumed.

---

# Verification

Every provider must implement

Verify Webhook

Verify Signature

Verify Authentication

Replay Protection

Timestamp Validation

Organization Resolution

---

# Organization Resolution

Every incoming request must resolve

Organization

before processing.

No event may enter the platform without an organization.

---

# Canonical Events

Publish

CustomerMessageReceived

CustomerMessageUpdated

CustomerMessageDeleted

ConversationStarted

ConversationClosed

ConversationAssigned

CustomerTyping

MediaUploaded

CallStarted

CallEnded

MessageReactionAdded

---

# Platform Events

Provider adapters publish

Platform Events

Only.

No module consumes provider events directly.

---

# Retry Policy

Retry

Transient failures

Do not retry

Authentication failures

Invalid signatures

Unknown organizations

Retries must be idempotent.

---

# Idempotency

Every provider message must be processed exactly once.

Store

Provider

External Message ID

Organization

Processed Timestamp

Duplicate events must be ignored.

---

# Security

Never trust provider payloads.

Always verify

Signature

Timestamp

Authentication

Replay attack

Organization

---

# Raw Payload

Always store

Raw payload

for debugging.

Business logic must never consume it.

---

# Media

Media downloads occur inside

Provider Adapter.

Business modules receive

Media Object

never provider URLs.

---

# AI Integration

AI Runtime consumes

Canonical Messages

AI never knows

whether the message originated from

WhatsApp

Instagram

Facebook

Website

Voice

---

# CRM Integration

CRM consumes

CustomerMessageReceived

Platform Event

Only.

---

# Booking Integration

Booking Workflow consumes

Canonical Messages

Only.

---

# Automation

Automation subscribes to

Platform Events.

Never provider payloads.

---

# Business Intelligence

BI subscribes to

Platform Events.

Not provider APIs.

---

# Provider Folder Structure

app/

providers/

meta/

whatsapp/

instagram/

facebook/

voice/

telegram/

shared/

Each provider owns only

adapter logic.

---

# n8n Responsibilities

n8n may

Receive webhook

Verify

Normalize

Publish Canonical Event

Forward to Zorovex

n8n must never contain

Business Rules

Booking Logic

CRM Logic

AI Decisions

Pricing Logic

---

# Future Providers

Adding a provider should require

One new adapter.

Nothing else.

---

# Acceptance Criteria

✓ Provider independent architecture

✓ Canonical event model

✓ Shared adapter interface

✓ Multi-tenant support

✓ Idempotent processing

✓ Secure verification

✓ Platform events only

✓ AI provider independent

✓ CRM provider independent

✓ Booking provider independent

---

# Consequences

Positive

Adding a new provider requires minimal work.

Business logic remains isolated.

Testing becomes simpler.

Provider failures remain contained.

Trade-offs

Requires additional abstraction.

Slightly more code.

Much easier long-term maintenance.

---

# Architect Notes

External providers are transport mechanisms.

They are not part of the business domain.

The business domain begins only after an incoming request has been verified, normalized and converted into a Canonical Event.

Every future integration must comply with this architecture.