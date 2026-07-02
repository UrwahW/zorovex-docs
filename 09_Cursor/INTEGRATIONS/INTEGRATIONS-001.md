# ENGINEERING TASK

ID

INTEGRATIONS-001

Sprint

Sprint 06

Title

Integration Platform & Provider Framework

Status

Approved

Depends On

ADR-013

PLATFORM-002

COMMS-001

AI-006

PATCH-001

---

# Objective

Implement the Zorovex Integration Platform.

The Integration Platform becomes the single gateway through which every external service communicates with the Business Operating System.

No module may communicate directly with provider APIs.

Every provider must pass through the Provider Framework before reaching the platform.

---

# Philosophy

External providers are transport layers.

Business logic begins only after an incoming request has been

- authenticated
- verified
- normalized
- converted into Canonical Events

The rest of Zorovex must never know whether an event originated from WhatsApp, Instagram, Facebook, Voice or any future provider.

---

# Required Reading

Before implementation read

1. ADR-013 – Integration Architecture
2. PLATFORM-002
3. COMMS-001
4. AI-006
5. PATCH-001

This PR implements the architecture defined in ADR-013.

---

# Scope

Implement

- Integration Platform
- Provider Registry
- Provider Framework
- Meta Adapter
- Incoming Event Pipeline
- Outgoing Event Pipeline
- Canonical Event Builder
- Retry Engine
- Dead Letter Queue
- Provider Health
- Integration Dashboard
- Integration Settings
- Integration Logs

---

# Architecture

External Provider

↓

Provider Adapter

↓

Webhook Verification

↓

Authentication

↓

Organization Resolution

↓

Normalization

↓

Canonical Event Builder

↓

Platform Event Bus

↓

Business Modules

↓

CRM

Bookings

AI

Automation

Business Intelligence

Audit

Notifications

---

# Supported Providers

Phase One

Meta

- WhatsApp
- Instagram
- Facebook Messenger

Website Chat

Future

Telegram

Voice

Email

SMS

Slack

Microsoft Teams

LinkedIn

Google Business Messages

TikTok

---

# Provider Registry

Create a registry responsible for

Provider Registration

Versioning

Capabilities

Authentication

Webhook Routes

Health Status

Configuration

Supported Channels

Providers must self-register.

No provider may be hardcoded.

---

# Provider Adapter

Every provider must implement

verifyWebhook()

verifySignature()

authenticate()

normalizeInbound()

sendOutbound()

downloadMedia()

resolveConversation()

healthCheck()

Provider adapters must contain no business logic.

---

# Meta Adapter

Create a shared Meta adapter.

WhatsApp

Instagram

Facebook Messenger

must share

Verification

Authentication

Retry Logic

Webhook Parsing

Signature Validation

Media Handling

Canonical Mapping

Only channel-specific behaviour should differ.

---

# Provider Configuration

Every organization configures

Provider Enabled

Credentials

Webhook Secret

API Tokens

Phone Number IDs

Business IDs

Supported Channels

Rate Limits

Feature Toggles

Configuration must remain organization scoped.

---

# Canonical Event Builder

Normalize every provider into one event model.

Supported Events

CustomerMessageReceived

CustomerMessageSent

CustomerMessageDelivered

CustomerMessageRead

CustomerTypingStarted

CustomerTypingStopped

ConversationStarted

ConversationAssigned

ConversationResolved

AttachmentReceived

AttachmentSent

CallStarted

CallEnded

VoiceMessageReceived

CustomerReactionAdded

CustomerReactionRemoved

CustomerBlocked

CustomerUnblocked

BusinessProfileUpdated

No module may consume provider payloads.

---

# Canonical Message

Every message contains

Organization ID

Provider

Channel

Conversation ID

Customer ID

External Customer ID

External Message ID

Timestamp

Direction

Message Type

Text

Attachments

Metadata

Raw Payload

Version

---

# Incoming Pipeline

Receive Webhook

↓

Verify Request

↓

Verify Signature

↓

Resolve Organization

↓

Normalize Payload

↓

Canonical Event

↓

Publish Platform Event

↓

Return Provider Response

---

# Outgoing Pipeline

Platform Event

↓

Provider Selection

↓

Provider Adapter

↓

Provider API

↓

Delivery Status

↓

Canonical Event

↓

Platform Event

---

# Organization Resolution

Every request must resolve

Organization

before processing.

Unknown organizations

must return a provider-safe error.

---

# Security

Every provider must verify

Webhook Token

Signature

Replay Attack

Timestamp

Organization

Credentials

Never trust provider payloads.

---

# Idempotency

Every inbound event must be processed exactly once.

Use

Organization

Provider

External Message ID

Duplicates must be ignored.

---

# Retry Engine

Automatically retry

Provider timeout

Temporary API failures

Network interruption

Do not retry

Invalid signatures

Unknown organizations

Authentication failures

Permanent validation failures

---

# Dead Letter Queue

Persist permanently failed events.

Display

Failure Reason

Retry Count

Payload

Provider

Organization

Timestamp

Manual Retry

---

# Integration Health

Track

Webhook Status

Authentication

Provider Availability

API Latency

Retry Count

Failed Deliveries

Duplicate Events

Dead Letter Queue Size

Last Successful Event

---

# Integration Dashboard

Display

Connected Providers

Organization Integrations

Health Status

Recent Events

Failed Events

Retry Queue

Provider Logs

Authentication Status

Webhook Status

Traffic

Latency

---

# Media Handling

Provider adapters download media.

Business modules receive

Media Objects

Never provider URLs.

Store

Media Type

Mime Type

Filename

Size

Preview

Storage Location

---

# AI Integration

AI Runtime consumes

Canonical Events only.

AI must never inspect provider payloads.

AI must never know whether the customer used

WhatsApp

Instagram

Facebook

Website

Voice

---

# CRM Integration

CRM listens for

CustomerMessageReceived

ConversationStarted

ConversationResolved

CustomerProfileUpdated

Platform Events only.

---

# Booking Integration

Booking Workflow consumes

Canonical Events only.

No provider-specific code.

---

# Automation

Automation subscribes to

Platform Events.

Never provider payloads.

---

# Business Intelligence

Business Intelligence subscribes to

Canonical Platform Events.

Never provider APIs.

---

# Notifications

Notifications consume

Platform Events.

Not provider events.

---

# Audit

Audit records

Verification

Authentication

Inbound

Outbound

Failures

Retries

Configuration Changes

Provider Health Changes

---

# n8n Responsibilities

n8n may

Receive Webhook

Verify Request

Normalize Payload

Forward Canonical Event

Nothing else.

n8n must never

Create Bookings

Update CRM

Execute AI

Apply Business Rules

Run Automations

Modify Database Records

---

# Folder Structure

backend/

app/

integrations/

providers/

meta/

shared/

registry/

events/

health/

retry/

dead_letter/

frontend/

features/

integrations/

dashboard/

providers/

health/

logs/

settings/

---

# Backend

Create

IntegrationPlatformService

ProviderRegistry

ProviderConfigurationService

MetaProviderAdapter

IntegrationHealthService

CanonicalEventBuilder

RetryService

DeadLetterService

MediaService

InboundPipeline

OutboundPipeline

Commands

Queries

Validators

Policies

Serializers

Factories

Specs

---

# Frontend

Create

Integration Dashboard

Provider Management

Provider Detail

Provider Health

Integration Logs

Retry Queue

Dead Letter Viewer

Configuration Pages

Webhook Status

Traffic Dashboard

---

# APIs

GET

/api/v1/integrations

GET

/api/v1/integrations/providers

GET

/api/v1/integrations/providers/:id

GET

/api/v1/integrations/health

GET

/api/v1/integrations/events

GET

/api/v1/integrations/dead-letter

POST

/api/v1/integrations/providers/:id/connect

POST

/api/v1/integrations/providers/:id/disconnect

POST

/api/v1/integrations/retry/:id

PATCH

/api/v1/integrations/providers/:id

---

# Permissions

Owner

Full Access

Manager

View

Reconnect

Retry Failed Events

Receptionist

No Access

Marketing

Read Provider Status

Accountant

Read Only

---

# Monitoring

Track

Webhook Verification

Signature Failures

Provider Errors

Retry Success Rate

Queue Size

Dead Letter Queue

Provider Latency

Provider Availability

Integration Throughput

---

# Logging

Log

Webhook Verified

Webhook Rejected

Signature Failed

Organization Resolved

Provider Connected

Provider Disconnected

Retry Started

Retry Completed

Retry Failed

Dead Letter Created

Dead Letter Resolved

Provider Health Changed

---

# Testing

Create

Provider Registry Specs

Meta Adapter Specs

Canonical Event Specs

Retry Specs

Dead Letter Specs

Health Specs

API Specs

Permission Specs

Frontend Specs

Integration Tests

All tests must pass.

---

# Deliverables

Integration Platform

Provider Framework

Meta Adapter

Provider Registry

Canonical Event Builder

Retry Engine

Dead Letter Queue

Integration Dashboard

REST APIs

Tests

Engineering Review

---

# Acceptance Criteria

✓ Integration Platform operational

✓ Provider Registry operational

✓ Meta Adapter operational

✓ Canonical Events operational

✓ Retry Engine operational

✓ Dead Letter Queue operational

✓ Integration Dashboard operational

✓ Multi-tenant configuration operational

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

98_Engineering_Reviews/Sprint-06/Reviews/INTEGRATIONS-001.md

Include

- Summary
- Files Created
- Files Modified
- Database Changes
- Provider Registry
- Meta Adapter
- Canonical Event Pipeline
- Retry Engine
- Dead Letter Queue
- Integration Dashboard
- API Endpoints
- Permissions
- Monitoring
- Logging
- Tests Added
- Assumptions
- Risks
- Technical Debt
- Future Providers

---

# Architect Notes

This PR implements the provider architecture defined in ADR-013.

Business modules must never communicate directly with external providers.

Every integration must pass through the Provider Framework and emit Canonical Events before entering the Business Operating System.

This PR establishes the permanent integration foundation for all current and future communication providers.