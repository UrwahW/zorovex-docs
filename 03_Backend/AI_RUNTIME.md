# AI Runtime

**Version:** 2.0

**Owner:** AI Platform

**Status:** Production Architecture

**Related Documents**

- AGENT_ARCHITECTURE.md
- KNOWLEDGE_SYSTEM.md
- BUSINESS_READINESS.md
- WORKFLOW_ENGINE.md
- TOOL_EXECUTION.md
- BUSINESS_CATALOG.md
- CHANNELS.md
- VOICE.md
- AI_OBSERVABILITY.md

---

# Purpose

The AI Runtime is the central intelligence orchestration engine of Zorovex.

It transforms customer interactions into deterministic business decisions and, when appropriate, natural language responses.

The Runtime is intentionally designed **not** to behave as a general-purpose chatbot.

Instead, it functions as the Business Operating Engine responsible for orchestrating business rules, commercial knowledge, workflows, tools, AI providers, validation, confidence, and escalation.

Every AI capability inside Zorovex executes through this Runtime.

---

# Vision

The Runtime acts as the operating system of the Zorovex AI Platform.

Its responsibilities are to:

- interpret customer requests
- understand business context
- enforce deterministic business rules
- retrieve authoritative knowledge
- coordinate workflows
- invoke tools
- generate conversational responses
- monitor execution
- explain every decision

Language models enhance communication.

They never own business logic.

---

# Runtime Ownership

The Runtime is the single authoritative orchestration layer of the AI Platform.

The Runtime owns:

- execution sequencing
- context construction
- business decision orchestration
- workflow selection
- tool coordination
- provider selection
- prompt compilation
- validation
- confidence calculation
- escalation
- observability
- runtime replay

The Runtime does **not** own:

- Business Catalog
- CRM
- Pricing
- Bookings
- AI Agent configuration
- Communication channels
- Provider credentials

Those responsibilities belong to their respective platform domains.

---

# Philosophy

The Runtime follows one fundamental principle.

> AI may generate language.
>
> AI must never generate business decisions.

Business decisions are deterministic.

Examples include:

- appointment availability
- service pricing
- promotions
- discounts
- memberships
- deposits
- cancellation policy
- refunds
- business hours
- holiday rules
- workflow selection
- ownership transfer
- feature entitlements

Every business decision is resolved before an AI provider executes.

The provider converts business decisions into conversational language.

---

# Runtime Principles

The Runtime always follows these architectural principles.

- Workflow First
- Business Rules Before AI
- Provider Independence
- Deterministic Decisions
- Explainable Outcomes
- Validation Before Delivery
- Tenant Isolation
- Runtime as Single Source of Orchestration Truth

No feature may bypass these principles.

---

# Responsibilities

The Runtime is responsible for:

- interpreting customer intent
- retrieving business knowledge
- enforcing business rules
- selecting workflows
- orchestrating providers
- validating responses
- determining confidence
- triggering escalations
- coordinating tools
- recording runtime telemetry

The Runtime is NOT responsible for:

- storing business data
- editing catalog records
- deciding commercial policy
- customer memory persistence
- communication transport
- external integrations

---

# Runtime Entry Points

Every AI interaction enters through exactly one interface.

```
AiRuntime.execute()
```

Current entry points

- AI Playground
- Runtime Execute API
- Website Chat
- WhatsApp
- Instagram
- Facebook Messenger
- Voice Calls
- Evaluations
- Replay
- Observability

Future

- Email
- SMS
- Marketplace Apps
- Public APIs

No channel owns separate AI logic.

---

# Channel Independence

Every communication channel executes through the identical Runtime pipeline.

```
Website Chat
        │
WhatsApp
        │
Instagram
        │
Facebook
        │
Voice
        │
Playground
        │
───────────────
     Runtime
───────────────
```

Channels transport messages.

The Runtime performs all intelligence.

---

# Runtime Architecture

```
Customer Message

↓

Context Builder

↓

Attachment Intelligence

↓

Intent Resolution

↓

Topic Guard

↓

Goal Resolution

↓

Business Rules

↓

Knowledge Retrieval

↓

Workflow Router

↓

Tool Selection

↓

Prompt Compilation

↓

Provider Execution

↓

Response Validation

↓

Confidence Calculation

↓

Escalation Engine

↓

Runtime Inspector

↓

Customer Response
```

Every execution follows this pipeline.

No stage may be skipped.

---

# Runtime Lifecycle

## Stage 1 — Incoming Request

Every execution creates:

- Execution ID
- Correlation ID
- Request ID
- Organization Context
- Actor Context
- Channel Context
- Execution Context

These identifiers remain attached throughout execution.

---

## Stage 2 — Context Building

The Runtime gathers:

- Organization
- Business Profile
- Business Catalog
- Business Readiness
- Customer
- Conversation
- Thread
- Staff
- Permissions
- Previous Messages
- Channel
- AI Agent Configuration

No provider is contacted during this stage.

---

## Stage 3 — Attachment Intelligence

Incoming attachments are classified.

Current support

- Images (metadata)
- Documents (metadata)
- Audio (metadata)

Future

```
Upload

↓

Classification

↓

OCR / Vision / Speech-to-Text

↓

Entity Extraction

↓

Review

↓

Published Business Records

↓

Knowledge Retrieval
```

Uploaded files never become authoritative knowledge automatically.

---

## Stage 4 — Intent Resolution

Determine customer intent.

Current implementation

Deterministic keyword-based resolver.

Future

Hybrid semantic resolver with deterministic verification.

Example intents

- Booking
- Reschedule
- Pricing
- Recommendation
- Complaint
- Refund
- Promotion
- Human Assistance
- Payment
- Availability

Intent must never rely solely on an LLM.

---

## Stage 5 — Topic Guard

Determines whether the request belongs within the business domain.

Allowed

- services
- bookings
- pricing
- promotions
- business information

Blocked

- homework
- coding
- politics
- general trivia
- unsafe requests

Blocked requests never invoke an AI provider.

---

## Stage 6 — Goal Resolution

Goals determine desired business outcomes.

Examples

- Answer Question
- Book Appointment
- Capture Lead
- Recommend Package
- Escalate
- Upsell

Goals are derived from:

- intent
- AI Agent configuration
- receptionist settings
- escalation rules

Goals never originate from the provider.

---

## Stage 7 — Business Rules

Business rules are authoritative.

Examples

- deposits
- holiday pricing
- memberships
- cancellation
- booking limits
- availability
- feature entitlements

Providers never evaluate policy.

---

## Stage 8 — Knowledge Retrieval

Knowledge is retrieved from structured business records.

Sources include

- Business Profile
- Business Catalog
- Services
- Categories
- Packages
- Promotions
- Pricing Rules
- Business Hours
- Staff
- Policies
- FAQs
- Business Notes

Knowledge retrieval is intent-aware.

Raw uploaded documents are never queried directly.

---

## Stage 9 — Workflow Routing

Deterministic workflows execute before providers.

Examples

- Booking
- Lead Capture
- Complaint
- Human Handoff
- Recommendations

Workflow responses may completely bypass provider generation.

---

## Stage 10 — Tool Selection

The Runtime identifies backend capabilities required.

Examples

- Booking Tool
- CRM Tool
- Customer Lookup
- Availability Tool
- Promotion Lookup

Current execution modes

- Simulated
- Executed
- Failed
- Skipped

Tool status is exposed through Runtime Inspector.

---

## Stage 11 — Prompt Compilation

Prompt compilation occurs only after business decisions are complete.

Prompt contains

- Business Context
- Knowledge
- Goals
- Behaviour
- Restrictions
- Conversation Context

Prompt never contains

- secrets
- platform configuration
- internal identifiers
- cross-tenant information

---

## Stage 12 — Provider Execution

Supported

- Mock
- OpenAI

Future

- Anthropic
- Gemini
- Azure OpenAI
- Local Models

Provider selection depends upon

- execution context
- channel
- organization
- explicit override
- environment

Providers generate language only.

---

# Provider Independence

Providers are interchangeable language engines.

The Runtime owns:

- intent
- goals
- workflows
- business rules
- validation
- confidence

Providers receive only compiled context.

Changing providers must never alter Runtime behaviour.

---

## Stage 13 — Response Validation

Every provider response is validated.

Checks include

- pricing
- availability
- promotions
- business hours
- booking confirmation
- policy claims

Unsafe responses are replaced with deterministic fallback messages.

Validation is deterministic.

---

## Stage 14 — Confidence

Confidence is calculated from Runtime signals.

Signals include

- intent quality
- knowledge coverage
- workflow execution
- validation status
- business completeness
- ambiguity

Confidence drives

- escalation
- observability
- evaluation
- analytics

Provider confidence is never trusted.

---

## Stage 15 — Escalation

Escalation decisions are deterministic.

Triggers

- low confidence
- complaints
- explicit human request
- missing knowledge
- policy uncertainty
- repeated misunderstanding
- payment issues

Escalation transfers ownership to a human.

---

# Runtime Modes

Supported modes

- Mock
- Workflow
- Provider
- Replay
- Evaluation
- Playground
- Production

Every mode shares identical orchestration.

Only execution context changes.

---

# Runtime Inspector

The Runtime Inspector exposes engineering telemetry.

Information includes

- intent
- goals
- knowledge
- workflow
- tools
- validation
- provider
- confidence
- execution mode
- escalation
- decision trace
- execution IDs

Business users receive simplified information.

Platform administrators receive full engineering telemetry.

---

# Observability

Every execution produces structured telemetry.

Examples

- Execution ID
- Correlation ID
- Latency
- Provider
- Workflow
- Intent
- Knowledge Coverage
- Validation Status
- Tool Status
- Confidence
- Escalation
- Decision Trace

Observability powers

- Replay
- Runtime Logs
- AI Evaluations
- Platform Analytics
- Support Sessions

---

# Security

The Runtime never exposes

- provider secrets
- API keys
- platform metadata
- cross-tenant data
- internal identifiers

Prompt compilation sanitizes every provider request.

---

# Performance

Execution minimizes provider calls.

Priority

```
Workflow

↓

Cache

↓

Knowledge

↓

Provider

↓

Validation
```

Future improvements

- streaming
- parallel retrieval
- vector search
- execution cache
- provider failover

---

# Scalability

The Runtime supports

- Multiple Organizations
- Multiple AI Agents
- Multiple Providers
- Multiple Channels
- Concurrent Executions
- Future Multi-Agent Collaboration

---

# Future Roadmap

AI-009

Customer Memory

AI-010

Vision

AI-011

Speech-to-Text

AI-012

Realtime Voice

AI-013

Real Tool Execution

AI-014

Multi-Agent Coordination

AI-015

Knowledge Embeddings

AI-016

Reasoning Providers

---

# Engineering Rules

- Never place business logic inside providers.
- Never allow providers to select workflows.
- Never allow providers to decide pricing or policies.
- Never bypass validation.
- Never bypass workflow routing.
- Never expose business secrets to providers.
- Never duplicate Runtime orchestration.
- Every AI feature must extend the existing Runtime.

The Runtime is the canonical intelligence engine of the Zorovex platform.

---

# Summary

The AI Runtime is the heart of the Zorovex AI Platform.

It transforms customer requests into deterministic business decisions while delegating natural language generation to interchangeable providers.

This separation guarantees explainability, auditability, scalability, provider independence, and long-term maintainability across every AI capability.

---

# Revision History

| Version | Date | Summary |
|----------|------|---------|
| 1.0 | Launch Sprint | Initial Runtime architecture |
| 2.0 | Launch Sprint | Expanded ownership, principles, observability, provider independence, Business Catalog integration, tool execution states, engineering standards |