# BUSINESS SETUP

Version: 1.0

Status: Approved

Sprint: 1

---

# Purpose

The Business Setup Wizard is responsible for onboarding a newly registered business into Zorovex.

Its purpose is to collect all information required for the CRM, Booking Engine, AI Receptionist, Calendar, and future modules.

Business Setup is completed once, but can be revisited at any time.

Every step is automatically saved.

---

# Goals

The setup process should:

- Be simple.
- Never overwhelm the business owner.
- Auto-save every change.
- Allow the owner to leave and return later.
- Show clear progress.
- Prevent entering the CRM until minimum setup is complete.

---

# Wizard Steps

Step 1

Business Identity

Step 2

Location

Step 3

Working Hours

Step 4

Services

Step 5

Staff

Step 6

Knowledge

Step 7

Communication Channels

Step 8

AI Receptionist

Step 9

Finish

---

# Auto Save

Every step must auto-save.

There is no global Save button.

Every successful save updates:

Last Updated

Completion Percentage

Current Step

---

# Progress

Progress is stored in:

business_setup_progress

Progress is calculated automatically.

Example

Business Identity

100%

Location

100%

Working Hours

50%

Overall

31%

---

# Resume

If the owner logs out:

The wizard resumes from the last unfinished step.

---

# Completion Rules

Minimum required before CRM access:

Business Identity

Location

One Service

One Staff Member

Working Hours

Everything else can be completed later.

---

# Navigation

Previous

Next

Exit

Resume

Cancel

No step can be skipped if it is required.

Optional steps may be skipped.

---

# Dashboard

Until setup is complete:

Dashboard shows:

Business Setup Progress

Continue Setup

Checklist

Recent Activity

No analytics.

---

# Permissions

Owner

Full Access

Manager

Can complete setup

Receptionist

No Access

Marketing

Read Only

Accountant

Read Only

---

# Events

BusinessSetupStarted

BusinessSetupStepCompleted

BusinessSetupCompleted

BusinessSetupUpdated

---

# Audit Logs

Every completed step creates an audit log.

---

# API

GET /api/v1/business/setup

Returns:

Current Step

Completion

Completed Steps

Remaining Steps

PATCH endpoints exist for each step.

One endpoint per step.

---

# UI Principles

Dark Theme

Minimal

Progress always visible

Auto-save indicator

Responsive

Keyboard friendly

Accessible

---

# Out of Scope

Booking

Customers

AI Runtime

Campaigns

Analytics

These are separate features.