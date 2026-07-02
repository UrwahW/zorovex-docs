# ENGINEERING TASK

ID

CORE-001

Sprint

Sprint 05

Title

Organization Platform

Status

Approved

Depends On

AUTH-001

PLATFORM-001

PLATFORM-002

---

# Objective

Implement the Organization Platform.

The Organization Platform becomes the canonical source of truth for every organization using Zorovex.

Every business belongs to exactly one Organization.

Every module reads organization information from this platform.

---

# Philosophy

Organization answers

"Who is this business?"

Business Settings answer

"How does this business operate?"

Never mix identity with operational configuration.

---

# Scope

Implement

- Organization Profile
- Branding
- Localization
- Timezone
- Currency
- Subscription
- Feature Flags
- Organization Lifecycle
- Organization Metadata
- Organization Preferences
- Organization Integrations
- Organization Health

---

# Organization Profile

Support

Business Name

Legal Name

Display Name

Logo

Cover Image

Website

Industry

Description

Registration Number

Tax Number

Email

Phone

Support Email

Support Phone

---

# Business Identity

Store

Organization UUID

Slug

Public Name

Internal Name

Created Date

Status

Owner

---

# Organization Status

Trial

Active

Suspended

Past Due

Cancelled

Archived

---

# Branding

Support

Primary Color

Secondary Color

Accent Color

Logo

Dark Logo

Favicon

Email Branding

Invoice Branding (future)

---

# Localization

Support

Timezone

Language

Date Format

Time Format

Currency

Currency Symbol

Number Format

Week Start Day

---

# Subscription

Track

Plan

Status

Billing Cycle

Renewal Date

Seats

Storage

AI Credits (future)

Usage Limits

---

# Feature Flags

Support

CRM

Bookings

Operations

Communications

AI

Automation

Business Intelligence

Calendar

Payments

Future Modules

Per Organization.

---

# Organization Metadata

Store

Industry

Business Size

Employee Count

Branch Count

Opening Date

Internal Notes

Tags

---

# Organization Lifecycle

Support

Create

Activate

Suspend

Archive

Restore

Delete (soft)

Transfer Ownership

---

# Integrations

Store connected providers

Google

Microsoft

Meta

Twilio

Future providers

Only store configuration references.

No provider logic.

---

# Organization Health

Track

Storage Usage

API Usage

AI Usage

Conversation Count

Booking Count

Automation Count

Errors

Warnings

Subscription Health

---

# APIs

GET /api/v1/organization

PATCH /api/v1/organization

GET /api/v1/organization/subscription

GET /api/v1/organization/features

PATCH /api/v1/organization/features

GET /api/v1/organization/integrations

---

# Backend

Create

OrganizationPlatformService

OrganizationLifecycleService

BrandingService

LocalizationService

FeatureFlagService

SubscriptionService

OrganizationHealthService

Policies

Commands

Queries

Validators

Serializers

Factories

Specs

---

# Frontend

Create

Organization Profile

Branding

Localization

Subscription

Feature Flags

Organization Health

Integration Overview

---

# Permissions

Owner

Full

Manager

Profile

Receptionist

Read

Marketing

Branding

Accountant

Subscription

---

# Domain Events

Publish

OrganizationCreated

OrganizationUpdated

OrganizationActivated

OrganizationSuspended

OrganizationArchived

SubscriptionChanged

FeatureFlagChanged

BrandingUpdated

LocalizationUpdated

---

# Logging

Log

OrganizationUpdated

SubscriptionUpdated

FeatureFlagUpdated

BrandingUpdated

LocalizationUpdated

---

# Testing

Create

Organization Specs

Branding Specs

Localization Specs

Feature Flag Specs

Subscription Specs

API Specs

Frontend Specs

All tests must pass.

---

# Deliverables

Organization Platform

Branding

Localization

Subscription

Feature Flags

REST APIs

Tests

Engineering Review

---

# Acceptance Criteria

✓ Organization Platform operational

✓ Branding operational

✓ Localization operational

✓ Subscription operational

✓ Feature Flags operational

✓ APIs operational

✓ Tests pass

✓ Rubocop passes

✓ Brakeman passes

Stop after completion.

Generate Engineering Review.

Wait for architect approval.

---

# Completion Report

Populate

98_Engineering_Reviews/Sprint-05/Reviews/CORE-001.md

Include

- Summary
- Files Created
- Files Modified
- Database Changes
- Organization Services
- APIs
- Domain Events
- Tests Added
- Assumptions
- Risks
- Technical Debt