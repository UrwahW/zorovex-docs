# ENGINEERING TASK

ID

PAYMENTS-001

Sprint

Sprint 05

Title

Business Payment Platform

Status

Approved

Depends On

BOOK-001

AI-005

AI-006

AUTO-001

PLATFORM-002

---

# Objective

Implement the Business Payment Platform.

The Payment Platform becomes the centralized payment domain for every financial interaction inside Zorovex.

It is responsible for business payment rules, payment requests, manual verification, payment lifecycle management and future payment provider integrations.

This module does NOT process payments directly.

Payment providers integrate through adapters.

---

# Philosophy

The business defines

How customers pay.

The platform manages

Payment requests.

Payment verification.

Payment lifecycle.

Future payment providers.

The Booking Engine and AI Runtime must never contain payment logic.

---

# Scope

Implement

- Payment Configuration
- Payment Requests
- Payment Verification
- Payment Lifecycle
- Payment Rules
- Payment Providers
- Payment Receipts
- Payment Timeline
- Refund Support
- Payment Events

---

# Architecture

Booking Workflow

↓

Payment Platform

↓

Business Rules

↓

Payment Provider

↓

Verification

↓

Workflow Resume

---

# Supported Payment Methods

Manual

Cash

Bank Transfer

Cheque

JazzCash

EasyPaisa

Raast

Custom Payment Link

Future

Stripe

PayPal

Apple Pay

Google Pay

Square

Authorize.Net

---

# Payment Configuration

Businesses configure

Accepted Methods

Currency

Deposit Required

Deposit Percentage

Deposit Amount

Manual Verification

Auto Verification (future)

Payment Instructions

Payment Expiration

Refund Policy

Late Payment Policy

Advance Payment Rules

---

# Payment Request

Support

Booking Deposit

Full Payment

Remaining Balance

Membership Payment (future)

Invoice Payment (future)

Custom Payment

---

# Payment Status

Pending

Waiting Customer

Waiting Verification

Verified

Rejected

Expired

Cancelled

Refunded

Partially Refunded

---

# Manual Verification

Support

Approve

Reject

Request Evidence

Upload Screenshot

Internal Notes

Verified By

Verified At

---

# Payment Timeline

Track

Created

Reminder Sent

Customer Uploaded Proof

Verified

Rejected

Refunded

Cancelled

Every event must appear on

Customer Timeline

Booking Timeline

Payment Timeline

Audit Timeline

---

# AI Integration

Workflow Engine reads

Business Payment Rules

↓

Requests Payment

↓

Waits

↓

Resumes Workflow

AI must never verify payments.

Only authorized users or future payment providers may verify payments.

---

# Booking Integration

Bookings may require

No Deposit

Percentage Deposit

Fixed Deposit

Full Payment

Payment rules determine booking progression.

---

# CRM Integration

Payments update

Customer Timeline

Last Payment Date

Payment History

Outstanding Balance (future)

---

# Automation Integration

Publish events

PaymentRequested

PaymentReminder

PaymentVerified

PaymentRejected

PaymentExpired

PaymentRefunded

---

# Domain Events

Publish

PaymentCreated

PaymentUpdated

PaymentVerified

PaymentRejected

PaymentExpired

PaymentRefunded

PaymentCancelled

---

# Providers

Create Provider Interface

Every provider implements

Create Payment

Check Status

Verify Payment

Refund Payment

Cancel Payment

Webhook (future)

---

# Provider Adapters

ManualProvider

JazzCashProvider

EasyPaisaProvider

RaastProvider

StripeProvider (future)

PayPalProvider (future)

---

# Payment Rules Engine

Support

Deposit Required

Percentage

Fixed Amount

Minimum Booking Amount

Service Specific Rules

Customer Specific Rules

Booking Source Rules

Future Membership Rules

---

# Refunds

Support

Full Refund

Partial Refund

Reason

Approved By

Refund Timeline

Future gateway refunds.

---

# APIs

GET /api/v1/payments

GET /api/v1/payments/:id

POST /api/v1/payments

PATCH /api/v1/payments/:id

POST /api/v1/payments/:id/verify

POST /api/v1/payments/:id/reject

POST /api/v1/payments/:id/refund

GET /api/v1/payment-settings

PATCH /api/v1/payment-settings

GET /api/v1/payment-methods

---

# Backend

Create

PaymentService

PaymentRequestService

PaymentVerificationService

PaymentRulesEngine

PaymentTimelineService

PaymentProviderRegistry

PaymentProvider

ManualPaymentProvider

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

Payment Dashboard

Payment Requests

Payment Verification

Payment Settings

Payment Timeline

Payment Methods

Refund Panel

Receipt Viewer

---

# Permissions

Owner

Full

Manager

Verify

Receptionist

Create Requests

Accountant

Verification

Marketing

Read Only

---

# Monitoring

Track

Pending Payments

Verification Time

Rejected Payments

Refund Rate

Deposit Collection Rate

Provider Availability

Future Gateway Metrics

---

# Logging

Log

PaymentCreated

PaymentRequested

PaymentVerified

PaymentRejected

PaymentExpired

PaymentRefunded

PaymentCancelled

---

# Testing

Create

Payment Rule Specs

Provider Specs

Verification Specs

Timeline Specs

API Specs

Frontend Specs

Automation Specs

All tests must pass.

---

# Deliverables

Business Payment Platform

Payment Rules

Provider Architecture

Manual Verification

Timeline

REST APIs

Tests

Engineering Review

---

# Acceptance Criteria

✓ Payment Platform operational

✓ Payment Rules operational

✓ Manual Verification operational

✓ Timeline operational

✓ Provider Architecture implemented

✓ Domain Events published

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

98_Engineering_Reviews/Sprint-05/Reviews/PAYMENTS-001.md

Include

- Summary
- Files Created
- Files Modified
- Database Changes
- Provider Architecture
- Payment Rules
- Timeline
- API Endpoints
- Domain Events
- Tests Added
- Assumptions
- Risks
- Technical Debt