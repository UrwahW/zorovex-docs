# ENGINEERING TASK

ID

PLATFORM-004

Sprint

Sprint 07

Title

Customer Onboarding & Workspace Provisioning

Status

Approved

Depends On

PLATFORM-003

AUTH-001

SETTINGS-001

CORE-001

---

# Objective

Create a complete customer onboarding platform.

Platform Administrators should be able to provision an entirely new customer workspace from the Platform Dashboard without manual database changes.

The customer should receive a secure invitation to activate their account.

Passwords must never be emailed.

---

# Philosophy

Creating a customer should provision an entire Business Operating System.

Not just a user account.

---

# Scope

Implement

Business Creation

Workspace Provisioning

Owner Invitation

Activation Flow

Provision Status

Onboarding Wizard

Welcome Emails

Invitation Management

---

# Business Creation

Platform Administrator enters

Business Name

Business Type

Owner Name

Owner Email

Owner Phone

Country

Timezone

Subscription Plan

Trial

Notes

No password.

---

# Workspace Provisioning

Automatically create

Organization

Owner User

Owner Role

Default Roles

Default AI Receptionist

Default Settings

Feature Flags

Knowledge Base

Business Calendar

Audit Record

Workspace

Provisioning should be atomic.

If provisioning fails

Rollback everything.

---

# Invitation Flow

Generate

Single-use Invitation Token

Expiration

7 Days

Invitation URL

Secure

Random

Cryptographically Generated

---

# Invitation Email

Send

Welcome

Organization Name

Activation Button

Support Contact

Documentation

No password.

---

# Activation

Customer

Creates Password

Accepts Terms

Activates Account

Automatically signs in.

---

# Invitation Management

Platform Admin can

Resend

Cancel

Regenerate

Copy Link

View Status

---

# Onboarding Status

Draft

Provisioning

Invited

Invitation Accepted

Active

Suspended

Cancelled

---

# First Login Wizard

Guide customer through

Business Profile

Business Hours

Services

Staff

Integrations

AI Knowledge

AI Test

Go Live

Progress must be saved.

---

# Welcome Tasks

Generate

Connect WhatsApp

Upload Knowledge

Add Staff

Create Services

Configure Payments

Complete Profile

Tasks disappear when completed.

---

# Emails

Workspace Created

Invitation Sent

Invitation Accepted

Welcome

Getting Started

Reminder (3 Days)

Reminder (6 Days)

Invitation Expired

---

# Backend

Create

WorkspaceProvisioningService

InvitationService

InvitationTokenService

OnboardingService

WelcomeTaskService

Commands

Queries

Validators

Policies

Serializers

Mailers

Jobs

---

# Frontend

Create

New Business Wizard

Invitation Status

Provision Progress

Activation Page

First Login Wizard

Welcome Dashboard

---

# APIs

POST

/api/v1/platform/businesses

GET

/api/v1/platform/businesses/:id

POST

/api/v1/platform/businesses/:id/invite

POST

/api/v1/platform/invitations/:token/activate

POST

/api/v1/platform/businesses/:id/resend

POST

/api/v1/platform/businesses/:id/cancel

---

# Security

Passwords

Never emailed

Never logged

Invitation Tokens

Single Use

Encrypted

Expiring

Audit Every Activation

---

# Testing

Provisioning

Rollback

Invitation

Activation

Wizard

Emails

Permissions

Welcome Tasks

All tests must pass.

---

# Deliverables

Business Provisioning

Workspace Provisioning

Invitation System

Activation Flow

First Login Wizard

Engineering Review

---

# Acceptance Criteria

✓ New business can be provisioned

✓ Workspace automatically created

✓ Secure invitation flow

✓ Owner chooses password

✓ Welcome wizard operational

✓ Tests pass

Stop after completion.

Generate Engineering Review.

Wait for architect approval.