# Security

Version 1.0

---

# Philosophy

Security is designed into the platform.

It is not added afterwards.

---

# Trust Boundaries

Browser

↓

API Gateway

↓

Rails

↓

Domain

↓

Database

↓

Infrastructure

---

# Authentication

JWT

Refresh Tokens

Session Revocation

Password Reset

2FA (future)

---

# Authorization

Policy based.

Never role checks in controllers.

Always

Policy

↓

Permission

↓

Decision

---

# Multi-tenancy

Every query scoped by organization.

Platform users require explicit bypass.

No shared customer data.

---

# Secrets

Never committed.

Environment variables only.

Production secrets managed externally.

---

# AI Security

LLM never receives

Internal IDs

Passwords

API Keys

Secrets

Platform data

Other organizations

---

# Prompt Security

Prompt Compiler

↓

Business Context

↓

Guardrails

↓

Provider

↓

Validation

---

# Input Validation

Every endpoint validates

Authentication

Authorization

Parameters

Business Rules

---

# File Uploads

Allowed

Images

Documents

Audio

Future

Video

Every upload

Virus Scan

Size Validation

Content Type Validation

Organization Ownership

Audit

---

# AI Uploads

Documents

↓

Storage

↓

Extraction

↓

Review

↓

Publish

Never

Document

↓

Production Data

---

# Logging

No passwords

No secrets

Sensitive tokens redacted.

---

# Audit

Every privileged action

User

Timestamp

Organization

Reason

Old Value

New Value

---

# Infrastructure

HTTPS only

TLS

Encrypted backups

Rate limiting

WAF (future)

---

# Future

Passkeys

Hardware Keys

Zero Trust

SOC2

ISO27001