# Permissions & Authorization

Version: 1.0

---

# Philosophy

Authentication answers:

Who are you?

Authorization answers:

What are you allowed to do?

Permissions are always determined on the backend.

Frontend permissions exist only for UX.

The frontend must never be trusted.

---

# Authorization Layers

Platform

↓

Organization

↓

Workspace

↓

Role

↓

Permission

↓

Policy

↓

Action

---

# Platform Roles

Platform Owner

Complete system control.

Can:

- Manage platform
- Delete organizations
- Billing
- Feature management
- Pricing
- Support sessions
- Platform analytics

---

Platform Administrator

Can manage organizations.

Cannot:

- delete platform
- change owner
- bypass audit logging

---

Support

Can impersonate organizations.

Cannot

- permanently modify subscriptions
- delete organizations

Default mode:

Read-only

---

Billing

Can

- manage subscriptions
- invoices
- payment status
- feature access

Cannot

- access customer conversations unless permitted

---

Developer

Engineering role.

Development only.

Never exists in production.

---

Customer Success

Can

- review readiness
- onboarding
- adoption
- health score

Cannot change commercial settings.

---

# Workspace Roles

Owner

Full control.

---

Manager

Business management.

Cannot delete organization.

---

Receptionist

Customers

Bookings

Conversations

Calendar

No catalog administration.

---

Stylist

Own appointments.

Own availability.

Limited customer visibility.

---

Marketing

Campaigns

Promotions

Analytics

No financial settings.

---

Finance

Invoices

Payments

Reports

No AI administration.

---

Read Only

View permissions only.

No writes.

---

# Permission Categories

Business

Catalog

Customers

Bookings

Staff

Payments

Communications

Knowledge

AI

Automation

Analytics

Administration

Platform

---

# Permission Naming

Every permission follows

resource.action

Examples

customers.read

customers.create

customers.update

customers.delete

bookings.manage

staff.assign

catalog.publish

catalog.import

pricing.manage

knowledge.publish

ai.configure

automation.manage

platform.organizations.manage

subscriptions.update

---

# Permission Resolution

Request

↓

Authentication

↓

Organization

↓

Workspace

↓

Role

↓

Permission Set

↓

Policy Check

↓

Allowed / Denied

---

# Policies

Policies contain business rules.

Example

Owner may delete services.

Receptionist may not.

Manager may edit pricing.

Stylist may not.

Never place business authorization inside controllers.

---

# Multi-tenancy Rules

Every permission is organization scoped.

Platform users operate outside tenant boundaries.

Workspace users cannot escape tenant boundaries.

---

# Audit Requirements

The following actions MUST be audited.

Catalog Publish

Pricing Change

Subscription Change

Role Assignment

Permission Changes

Support Session

Business Deletion

AI Configuration

Feature Overrides

---

# Future

Attribute-based permissions

Delegated administration

Temporary permissions

Approval workflows