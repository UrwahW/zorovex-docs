# Coding Standards

---

# Philosophy

Code should explain business.

Not implementation.

Readable beats clever.

Consistency beats preference.

---

# Architecture

Controllers

Thin

↓

Application Services

↓

Domain Services

↓

Repositories

↓

Persistence

Controllers never contain business logic.

---

# Naming

Prefer

BusinessService

CatalogPublishService

BookingWorkflow

Avoid

Helper

Utils

Manager

Processor

Engine

unless they truly represent those concepts.

---

# Service Rules

One responsibility.

Small public interface.

Deterministic.

Composable.

Testable.

---

# Events

Emit after successful state changes.

Never before persistence.

---

# AI

Providers generate language.

Ruby decides business.

Never reverse this rule.

---

# Models

Models own relationships.

Not workflows.

Not orchestration.

---

# Background Jobs

Retry safe.

Idempotent.

No UI assumptions.

---

# APIs

REST

Versioned

Consistent errors

Consistent pagination

Stable contracts

---

# Logging

Structured.

Searchable.

Correlation IDs.

No string concatenation logs.

---

# Testing Pyramid

Unit

↓

Service

↓

Request

↓

Integration

↓

End-to-End

---

# Documentation

Every architectural decision

↓

Documentation first

↓

Implementation second

---

# Pull Requests

Every PR includes

Purpose

Architecture

API Changes

Events

Security

Migration

Testing

Future Work

---

# Review Checklist

Business logic isolated

Permissions checked

Events emitted

Audited

Tests added

Documentation updated

---

# Future

ADR references

Automatic architecture validation

Static dependency rules