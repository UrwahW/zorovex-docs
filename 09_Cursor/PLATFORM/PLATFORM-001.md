# ENGINEERING TASK

ID

PLATFORM-001

Sprint

Sprint 4

Title

Platform Foundation

Status

Approved

Depends On

COMMS-001

---

# Read First

Before implementation, read:

1. 09_Cursor/START_HERE.md
2. 09_Cursor/Cursor_Rules.md
3. 09_Cursor/DOCUMENTATION_AUTOMATION.md

Do not begin until these have been reviewed.

---

# Objective

Implement the platform foundation for Zorovex.

This PR creates the shared platform services used by AI, Communications, Reports, Automations and future Billing.

This task does NOT implement:

- Billing
- Stripe
- Paddle
- LemonSqueezy
- Payments

This task prepares the platform for those integrations.

---

# Scope

Implement

- Organization Status
- Organization Plans
- Platform Context
- Feature Registry
- Feature Access Service
- Channel Registry
- Channel Access Service
- Super Admin Foundation
- Organization Feature Policy
- Platform Logging

---

# Database

Extend organizations

Add

plan

status

trial_ends_at

grace_ends_at

suspended_at

suspension_reason

created_at

updated_at

---

# Organization Status

Supported values

trial

active

grace_period

suspended

inactive

---

# Organization Plans

starter

professional

enterprise

custom

---

# Feature Registry

Create a central registry.

Supported features

crm

bookings

operations

communications

ai_runtime

ai_actions

whatsapp

instagram

facebook

website_chat

voice

reports

automations

api_access

Future features must register here.

No hardcoded feature strings anywhere else.

---

# Channel Registry

Supported channels

website_chat

whatsapp

instagram

facebook

voice

Future channels

email

sms

must be added here.

---

# Platform Context

Create

PlatformContext

Purpose

Provide every module with a single platform snapshot.

Expose

organization

plan

status

features

channels

ai_enabled?

channel_enabled?(channel)

feature_enabled?(feature)

trial?

grace_period?

suspended?

No module should directly inspect organization status.

---

# Feature Access Service

Create

Platform::FeatureAccessService

Public API

check(
organization:,
feature:
)

Returns

FeatureAccessResult

Expose

allowed?

reason

feature

organization

Never raise exceptions.

---

# Supported Reasons

allowed

trial

subscription_required

organization_suspended

organization_inactive

feature_not_in_plan

system_disabled

---

# Channel Access Service

Create

Platform::ChannelAccessService

Public API

check(
organization:,
channel:
)

Returns

ChannelAccessResult

Supported channels

website_chat

whatsapp

instagram

facebook

voice

---

# Organization Feature Policy

Centralize all feature availability.

No module should implement subscription logic.

No module should inspect plans.

No module should inspect organization status.

Everything routes through this policy.

---

# Super Admin Foundation

Create platform role

Super Admin

Capabilities

View Organizations

Suspend Organization

Activate Organization

Change Plan

Enable Feature

Disable Feature

Enable Channel

Disable Channel

View Platform Statistics

View AI Usage

View Communication Usage

No frontend required.

Backend only.

---

# Platform Logging

Log

OrganizationActivated

OrganizationSuspended

PlanChanged

FeatureEnabled

FeatureDisabled

ChannelEnabled

ChannelDisabled

FeatureDenied

Include

Organization

Actor

Timestamp

Reason

---

# AI Runtime Integration

Prepare integration only.

AI Runtime must use

FeatureAccessService

before processing conversations.

Do not implement AI Runtime.

---

# Communications Integration

Prepare integration only.

Communications must use

ChannelAccessService

before sending messages.

Do not modify provider integrations.

---

# Backend

Create

PlatformContext

FeatureRegistry

ChannelRegistry

FeatureAccessService

ChannelAccessService

OrganizationFeaturePolicy

Platform Types

Platform Serializer

Platform Policy

Factories

Validators

Request Specs

Policy Specs

Service Specs

---

# API

GET

/api/v1/platform/context

Returns

organization status

plan

enabled features

enabled channels

Current authenticated organization only.

No admin endpoints in this PR.

---

# Permissions

Owner

View platform context

Manager

View platform context

Receptionist

No access

Marketing

No access

Accountant

No access

Super Admin

Full platform access

---

# Testing

Create

Platform Context Specs

Feature Registry Specs

Channel Registry Specs

Feature Access Specs

Channel Access Specs

Organization Feature Policy Specs

Platform Request Specs

All tests must pass.

---

# Logging

Every denied feature request

must create

FeatureDenied

Every denied channel request

must create

ChannelDenied

---

# Out of Scope

Billing

Invoices

Payments

Stripe

Paddle

LemonSqueezy

Usage Metering

Customer Portal

Subscription Management

Multi Organization Switching

---

# Deliverables

Platform Context

Organization Plans

Organization Status

Feature Registry

Channel Registry

Feature Access Service

Channel Access Service

Platform Policy

Super Admin Foundation

Tests

Documentation Updates

Engineering Review

---

# Acceptance Criteria

✓ Platform Context implemented

✓ Feature Registry implemented

✓ Channel Registry implemented

✓ Feature Access Service implemented

✓ Channel Access Service implemented

✓ Organization plans implemented

✓ Organization statuses implemented

✓ AI Runtime ready

✓ Communications ready

✓ Tests pass

✓ Rubocop passes

✓ Brakeman passes

Stop after completion.

Do not continue to AI-004.

Wait for architect approval.

---

# Completion Report

Populate

98_Engineering_Reviews/Sprint-04/Reviews/PLATFORM-001.md

Provide

Summary

Files Created

Files Modified

Database Changes

API Endpoints

Services Added

Tests Added

Assumptions

Suggestions

Blockers

Do not continue to AI-004 until architect approval.