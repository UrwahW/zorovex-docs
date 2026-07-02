# ENGINEERING TASK

ID

PLATFORM-003

Sprint

Sprint 07

Title

Platform Administration & Support Workspace

Status

Approved

Depends On

PLATFORM-001

PLATFORM-002

CORE-001

SETTINGS-001

INTEGRATIONS-001

---

# Objective

Build the internal Platform Administration Workspace used exclusively by the Zorovex team.

This workspace allows Platform Administrators to manage customer organizations, provide support, configure workspaces, control subscriptions and safely access customer environments.

This workspace is NOT available to customer organizations.

---

# Philosophy

Platform Administrators manage the SaaS platform.

Organization Owners manage their business.

These responsibilities must remain completely separated.

---

# Required Reading

Read before implementation

00_START_HERE.md

IMPLEMENTATION-STANDARDS.md

ADR-001

ADR-013

PLATFORM-001

---

# Scope

Implement

Platform Workspace

Organization Management

Support Sessions

Workspace Access

Module Management

Feature Flags

Subscription Controls

Organization Health

Provider Health

Audit Logs

---

# Organization Directory

Display

Business Name

Owner

Plan

Status

Health

Created Date

Last Activity

AI Status

Connected Providers

Unread Escalations

Last Login

Quick Search

Filters

Pagination

---

# Organization Workspace

Platform Admin can open

Customer Workspace

without logging in as that customer.

Access occurs through a

Support Session.

---

# Support Sessions

Implement

Create Session

Read Only Mode

Full Support Mode

Reason Required

Start Time

End Time

Session Timeout

Session Logs

Session History

Customer Visibility

Every support session must be audited.

---

# Workspace Access

Platform Admin can

Open Workspace

View Dashboard

View Customers

View Bookings

View AI

View Integrations

View Reports

Depending on selected support mode.

---

# Module Management

Enable

Disable

CRM

Bookings

Communications

AI

Operations

Business Intelligence

Marketing

Inventory (Future)

POS (Future)

Per Organization.

---

# AI Controls

Enable AI

Disable AI

Pause AI

Disable AI Actions

Force Human Only

View AI Health

Reset AI Knowledge Cache

---

# Subscription Controls

Trial

Professional

Enterprise

Custom

Suspend

Reactivate

Cancel

Grace Period

Expiry

Renew

---

# Feature Flags

Per Organization

Experimental Features

Voice

AI Employees

Automation

Integrations

Mobile App

Beta Features

Future Features

---

# Organization Health

Display

AI Health

Provider Health

Failed Automations

Dead Letters

Escalation Volume

Provider Status

Subscription Status

Storage Usage

API Usage

Message Volume

---

# Audit

Audit

Support Sessions

Configuration Changes

Feature Changes

Subscription Changes

AI Changes

Workspace Access

Every action must be recorded.

---

# Permissions

Platform Administrator

Full Access

Platform Support

Support Sessions

Read Only

Billing Team

Subscription Only

Developer

Read Only

Customer roles must never access this workspace.

---

# Backend

Create

Platform Workspace

Organization Management

Support Session Service

Workspace Access Service

Organization Health Service

Commands

Queries

Validators

Policies

Serializers

Audit Events

---

# Frontend

Create

Platform Dashboard

Organization List

Organization Details

Support Session Panel

Feature Flag Panel

Subscription Panel

Health Dashboard

---

# APIs

GET

/api/v1/platform/organizations

GET

/api/v1/platform/organizations/:id

POST

/api/v1/platform/organizations/:id/support

POST

/api/v1/platform/organizations/:id/end_support

PATCH

/api/v1/platform/organizations/:id/modules

PATCH

/api/v1/platform/organizations/:id/features

PATCH

/api/v1/platform/organizations/:id/subscription

---

# Constraints

Never impersonate users by changing authentication.

Support Sessions must preserve Platform Admin identity.

Every action must be attributable to the Platform Administrator.

---

# Testing

Support Session

Permissions

Audit

Organization Access

Feature Flags

Subscription

Health

Workspace Access

All tests must pass.

---

# Deliverables

Platform Administration Workspace

Support Sessions

Organization Management

Module Controls

Subscription Controls

Health Dashboard

Engineering Review

---

# Acceptance Criteria

✓ Platform Administration operational

✓ Secure Support Sessions

✓ Full audit logging

✓ Module management

✓ Subscription management

✓ Health monitoring

✓ Tests pass

Stop after completion.

Generate Engineering Review.

Wait for architect approval.