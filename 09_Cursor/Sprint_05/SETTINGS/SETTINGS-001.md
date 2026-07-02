# ENGINEERING TASK

ID

SETTINGS-001

Sprint

Sprint 05

Title

Business Configuration Platform

Status

Approved

Depends On

CORE-001

PAYMENTS-001

CALENDAR-001

AUTO-001

AI-007

---

# Objective

Implement the Business Configuration Platform.

This module defines **how an organization operates**. It centralizes all configurable business rules so that every module (Bookings, AI, CRM, Calendar, Payments, Automations, etc.) reads behavior from one place.

---

# Philosophy

Organization Platform defines **who the business is**.

Business Configuration defines **how the business works**.

No operational rules should live inside feature modules.

---

# Scope

Implement

- Working Hours
- Booking Rules
- Cancellation Rules
- Payment Defaults
- AI Defaults
- Staff Defaults
- Communication Defaults
- Automation Defaults
- Service Defaults
- Business Policies
- Configuration Templates

---

# Working Hours

Support

Business Hours

Department Hours (future)

Staff Overrides

Breaks

Lunch

Holidays

Blackout Dates

Emergency Closures

---

# Booking Rules

Support

Minimum Notice

Maximum Advance Booking

Buffer Time

Maximum Daily Bookings

Maximum Concurrent Bookings

Walk-in Rules

Online Booking Toggle

AI Booking Toggle

---

# Cancellation Rules

Support

Cancellation Window

Late Cancellation Policy

No-show Policy

Refund Eligibility

Reschedule Limits

---

# Payment Defaults

Support

Default Deposit Rule

Default Payment Method

Payment Expiration

Manual Verification Requirement

---

# AI Defaults

Support

AI Enabled

AI Confidence Threshold

Human Handoff Threshold

Business Closed Behaviour

Greeting Templates

Knowledge Behaviour

Escalation Rules

---

# Communication Defaults

Support

Preferred Channels

Auto Replies

Business Hours Messages

Typing Indicators

Read Receipts

---

# Staff Defaults

Support

Default Availability

Booking Limits

Break Rules

Assignment Strategy

---

# Automation Defaults

Support

Enabled Automations

Default Templates

Retry Policy

Quiet Hours

---

# Service Defaults

Support

Default Duration

Preparation Time

Cleanup Time

Price Visibility

Online Availability

---

# Configuration Templates

Allow organizations to

Export Configuration

Import Configuration

Clone Configuration

Reset to Defaults

---

# APIs

GET /api/v1/settings

PATCH /api/v1/settings

GET /api/v1/settings/templates

POST /api/v1/settings/import

GET /api/v1/settings/export

---

# Backend

Create

BusinessConfigurationService

BookingRulesService

AIDefaultsService

CommunicationDefaultsService

AutomationDefaultsService

WorkingHoursService

ConfigurationTemplateService

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

Business Settings Dashboard

Working Hours

Booking Rules

AI Configuration

Communication Settings

Automation Settings

Import / Export

Configuration Templates

---

# Domain Events

Publish

SettingsUpdated

WorkingHoursUpdated

BookingRulesUpdated

AIDefaultsUpdated

CommunicationDefaultsUpdated

AutomationDefaultsUpdated

---

# Logging

Log

BusinessConfigurationUpdated

BookingRulesChanged

AIDefaultsChanged

WorkingHoursChanged

---

# Testing

Create

Configuration Specs

Working Hours Specs

Booking Rule Specs

AI Settings Specs

Import/Export Specs

API Specs

Frontend Specs

All tests must pass.

---

# Deliverables

Business Configuration Platform

Configuration Services

REST APIs

Templates

Import / Export

Tests

Engineering Review

---

# Acceptance Criteria

✓ Business Configuration operational

✓ Working Hours operational

✓ Booking Rules operational

✓ AI Defaults operational

✓ Configuration Templates operational

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

98_Engineering_Reviews/Sprint-05/Reviews/SETTINGS-001.md

Include

- Summary
- Files Created
- Files Modified
- Configuration Areas
- APIs
- Domain Events
- Tests Added
- Assumptions
- Risks
- Technical Debt