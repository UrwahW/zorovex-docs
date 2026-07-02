# ENGINEERING TASK

ID

AUTH-003

Sprint

Sprint 1

Title

Implement Organization & Organization Membership Domain

Status

Approved

---

# Read First

Before implementation, read:

1. 09_Cursor/START_HERE.md
2. 09_Cursor/Cursor_Rules.md
3. 02_Architecture/TECH_STACK.md
4. 03_Backend/AUTHENTICATION.md
5. 03_Backend/ORGANIZATIONS.md

Do not start coding until these documents have been reviewed.

---

# Objective

Implement the Organization Domain and Organization Membership Domain.

This task establishes the relationship between Users and Organizations.

Users DO NOT belong directly to organizations.

Users belong to organizations through memberships.

This architecture is locked.

---

# Scope

Implement ONLY:

- Organization model
- Organization migration
- OrganizationMembership model
- OrganizationMembership migration
- Associations
- Validations
- Factories
- Tests

Do not implement authentication.

Do not implement registration.

Do not implement roles.

Do not implement permissions.

---

# Organization Database

Create table:

organizations

Columns

id

UUID Primary Key

name

string

required

slug

string

required

unique

status

integer

default active

subscription_plan

string

default starter

subscription_status

integer

default trial

trial_ends_at

datetime

created_at

updated_at

---

# Organization Indexes

Unique

slug

Index

status

subscription_status

---

# Organization Model

Location

domains/organization/models/organization.rb

---

# Organization Validations

Validate

name

slug

status

subscription_plan

subscription_status

---

# Organization Slug

Automatically generate slug from organization name.

Slug must be unique.

Example

Glow Studio

↓

glow-studio

---

# Subscription Status Enum

trial

active

past_due

cancelled

suspended

---

# Organization Status Enum

active

inactive

archived

---

# Membership Database

Create table

organization_memberships

Columns

id

UUID Primary Key

organization_id

UUID

user_id

UUID

status

integer

default active

joined_at

datetime

last_accessed_at

datetime

created_at

updated_at

---

# Membership Indexes

organization_id

user_id

Unique

organization_id + user_id

---

# Membership Associations

Organization

has_many memberships

has_many users through memberships

User

has_many memberships

has_many organizations through memberships

OrganizationMembership

belongs_to user

belongs_to organization

---

# Membership Status

active

invited

inactive

removed

---

# Business Rules

A user may belong to multiple organizations.

An organization may contain multiple users.

Duplicate memberships are not allowed.

Membership deletion should use status instead of deleting records.

---

# Controllers

Do not create.

---

# API

Do not create.

---

# Authentication

Do not implement.

---

# Roles

Do not implement.

---

# Permissions

Do not implement.

---

# Factories

Create:

Organization Factory

OrganizationMembership Factory

---

# Tests

Create:

Organization model tests

Membership model tests

Association tests

Validation tests

Slug generation tests

Factory tests

Unique membership tests

All tests must pass.

---

# Documentation

Do not modify architecture.

Update backend documentation only if implementation requires clarification.

---

# Code Quality

Follow project coding standards.

Follow Rubocop.

Follow Brakeman.

Readable code.

No duplicate logic.

---

# Out of Scope

Do NOT implement:

Registration

JWT

Login

Sessions

Roles

Permissions

Business Profile

Business Setup

Staff

Customers

Anything outside Organization and Membership.

---

# Deliverables

Organization model

Organization migration

OrganizationMembership model

OrganizationMembership migration

Factories

Associations

Validation

Tests

---

# Acceptance Criteria

✓ Organization migration succeeds

✓ Membership migration succeeds

✓ Associations work

✓ Slug generation works

✓ Duplicate memberships rejected

✓ Factories pass

✓ Tests pass

✓ Rubocop passes

✓ Brakeman passes

Stop after the Definition of Done.

Do not continue to AUTH-004.

---

# Completion Report

Provide:

Summary

Files Created

Files Modified

Database Changes

Tests Added

Assumptions

Suggestions

Blockers