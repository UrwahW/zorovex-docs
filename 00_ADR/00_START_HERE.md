# ZOROVEX
# START HERE

Version

1.0

Last Updated

2026-06-30

---

# Purpose

This document is the mandatory entry point for every engineer and AI assistant working on Zorovex.

Before implementing any feature, bug fix or architectural change, read the required documents in the order defined below.

Do not begin implementation until the required documentation has been reviewed.

---

# What is Zorovex?

Zorovex is an AI Business Operating System.

It is NOT

- a CRM
- a Booking System
- an AI Chatbot
- a Salon Management System

Those are modules inside the platform.

Every implementation decision must reinforce the vision of Zorovex as one unified operating system.

---

# Documentation Reading Order

Always read documents in this order.

## Step 1

Read

README.md

Understand

- project purpose
- setup
- development workflow

---

## Step 2

Read

Vision.md

Understand

- long-term product vision
- AI strategy
- business goals

---

## Step 3

Read

Implementation Standards

05_Engineering/IMPLEMENTATION-STANDARDS.md

These rules apply to every PR.

---

## Step 4

Read all Architecture Decision Records (ADRs)

08_Architecture/ADR/

Read in numerical order.

Every ADR is authoritative.

If two documents conflict

ADR wins

unless a newer ADR explicitly replaces it.

---

## Step 5

Read previous engineering tasks related to the feature.

Example

Implementing AI

↓

Read

AI-001

↓

AI-002

↓

AI-003

↓

AI-004

↓

AI-005

↓

AI-006

↓

Current PR

Never implement a feature without understanding its predecessors.

---

## Step 6

Read the Engineering Review for the most recent implementation of the module.

Reviews often contain

- implementation decisions
- assumptions
- technical debt
- deviations

Do not repeat previously identified issues.

---

## Step 7

Read the current Engineering Task (PR).

Do not begin coding until all previous steps are complete.

---

# Engineering Principles

Every implementation must follow these principles.

## Multi-Tenant

Everything is organization scoped.

Never create global business data.

---

## Event Driven

Business modules communicate using Platform Events.

Never tightly couple unrelated modules.

---

## Domain Driven

Business logic belongs inside domains.

Controllers coordinate.

Services execute.

Commands mutate.

Queries retrieve.

Validators validate.

Policies authorize.

Serializers present.

---

## AI First

AI is a first-class employee.

Business workflows must support AI participation.

Do not special-case AI logic throughout the application.

---

## Provider Independence

Business modules never communicate directly with

- Meta
- Twilio
- Stripe
- Google
- Microsoft

Always communicate through Provider Adapters and Canonical Events.

---

## UI Philosophy

The application is one workspace.

Never design isolated module experiences.

Users should always remain in context.

---

# Before Writing Code

Produce an implementation plan.

The implementation plan must include

- architecture overview
- files to create
- files to modify
- migrations
- backend implementation order
- frontend implementation order
- testing strategy
- risks
- assumptions

Do not begin implementation until the plan is approved.

---

# During Implementation

Never

- rewrite unrelated code
- refactor outside scope
- weaken authorization
- bypass architecture
- duplicate business logic

Always reuse existing patterns where possible.

---

# After Implementation

Generate an Engineering Review containing

- Summary
- Files Created
- Files Modified
- Database Changes
- APIs
- Domain Events
- Permissions
- Tests
- Assumptions
- Risks
- Technical Debt
- Future Improvements

---

# Architect Review

After every implementation

STOP.

Do not continue with the next PR.

Wait for Architect Approval.

---

# Project Status

Current Phase

Sprint 06

Current Objective

Complete MVP

Upcoming Milestones

1. CORE-001
2. SETTINGS-001
3. UI-001
4. INTEGRATIONS-001
5. STABILIZATION-001
6. QA-001
7. Closed Beta

Future Roadmap

- AI-008
- AI-009
- AI-010
- COPILOT-001
- Marketing Platform
- Inventory
- POS
- Marketplace
- Mobile Apps

---

# Success Criteria

Every implementation should move Zorovex closer to becoming the world's leading AI Business Operating System.

If an implementation does not support this vision, reconsider the approach before writing code.