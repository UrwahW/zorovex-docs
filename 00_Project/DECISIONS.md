# Zorovex Architectural Decisions

Version: 1.0
Status: Living Document

---

# Purpose

This document records permanent architectural decisions that define how
Zorovex is built.

These decisions exist so future contributors understand **why** the
system works the way it does instead of only **how** it is implemented.

Every major architectural decision should be documented here before
implementation.

---

# ADR-001
## Deterministic AI over Autonomous AI

Status

Accepted

Reason

Zorovex is a business operating system.

Businesses require predictable decisions.

Appointment booking, pricing, cancellation policies,
refunds, deposits and availability cannot be delegated to
an LLM.

Decision

Business decisions are always resolved by deterministic
backend services.

The LLM is responsible only for language generation.

Consequences

Pros

• Predictable
• Auditable
• Explainable
• Easier debugging
• Lower legal risk

Cons

• More engineering effort
• Less "creative" AI

---

# ADR-002
## Business Data is the Source of Truth

Status

Accepted

Decision

The AI never owns business knowledge.

Authoritative data always lives inside structured business
domains.

Examples

Services

BusinessServices

Packages

BusinessPackages

Pricing

PricingRules

Hours

BusinessAvailability

Promotions

BusinessPromotions

Policies

BusinessKnowledge

AI reads these domains.

AI never replaces them.

---

# ADR-003
## AI Never Publishes Data

Status

Accepted

Decision

AI may detect

• services
• packages
• promotions
• holidays

AI produces suggestions.

Only deterministic services may publish data into the
Business Catalog after owner approval.

---

# ADR-004
## Multi Tenant First

Every organization is completely isolated.

Nothing is shared except platform infrastructure.

Each organization owns

• customers
• AI
• catalog
• conversations
• channels
• bookings
• automations

---

# ADR-005
## Platform vs Workspace

Platform Console

Manages organizations.

Business Workspace

Runs a single business.

Platform users never use Workspace
for administration.

Workspace users never access Platform.

---

# ADR-006
## Business Readiness is Computed

Readiness is never stored.

It is calculated from live business capabilities.

Readiness drives

• onboarding
• AI
• customer success
• platform analytics

---

# ADR-007
## Catalog is Commercial Truth

Services

Packages

Promotions

Pricing Rules

Holiday Rules

Categories

belong to the Business Catalog.

Knowledge is not the commercial catalog.

---

# ADR-008
## AI Entry Points Share One Runtime

Playground

Runtime

WhatsApp

Instagram

Facebook

Voice

Evaluations

all execute through

AiRuntime.execute()

No duplicated AI implementations exist.

---

# ADR-009
## Documents are Inputs

Documents are never business truth.

Pipeline

Document

↓

Extraction

↓

Review

↓

Published Records

---

# ADR-010
## Workflows Before LLM

Whenever a workflow can complete a task,
the workflow executes.

The LLM only fills conversational gaps.

---

Future ADRs

ADR-011 Voice Intelligence

ADR-012 Customer Memory

ADR-013 AI Agents

ADR-014 Marketplace

ADR-015 Enterprise Features