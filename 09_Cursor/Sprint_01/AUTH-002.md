# ENGINEERING TASK

ID

AUTH-002

Sprint

Sprint 1

Title

Implement User Identity Domain

Status

Approved

---

# Read First

Before implementation, read:

1. 09_Cursor/START_HERE.md
2. 09_Cursor/Cursor_Rules.md
3. 02_Architecture/TECH_STACK.md
4. 02_Architecture/SYSTEM_ARCHITECTURE.md
5. 02_Architecture/CODING_STANDARDS.md
6. 03_Backend/AUTHENTICATION.md

---

# Objective

Implement the User Identity domain.

The User represents a person's identity only.

A User does NOT belong directly to an Organization.

Relationships with organizations will be handled through Organization Memberships in AUTH-003.

This task only creates the User identity.

Nothing else.

---

# Scope

Implement ONLY:

- User migration
- User model
- UUID
- Validations
- Normalization
- Factory
- Tests

Do not implement authentication.

Do not implement memberships.

Do not implement organizations.

---

# Database

Create migration:

users

Columns

id

UUID Primary Key

first_name

string

required

last_name

string

required

email

string

required

unique

phone

string

nullable

password_digest

string

required

avatar_url

text

nullable

email_verified_at

datetime

nullable

last_login_at

datetime

nullable

status

integer

default active

created_at

updated_at

---

# Indexes

Create:

Unique index on email

Index on status

---

# UUID

Use UUID as the primary key.

Do not use integer IDs.

---

# Model

Create:

User

Location

domains/identity/models/user.rb

---

# Associations

Do NOT create any belongs_to relationship.

Do NOT reference organizations.

Do NOT reference memberships.

Associations will be added later.

---

# Validations

Validate:

first_name

last_name

email

password_digest

status

Email must be unique.

---

# Email Normalization

Before validation:

Strip whitespace.

Convert to lowercase.

Example

" John@Example.COM "

becomes

john@example.com

---

# Enum

status

active

inactive

suspended

deleted

---

# Business Rules

A User represents a human identity.

A User can eventually belong to multiple organizations.

A User can exist before belonging to an organization.

Never hardcode organization relationships here.

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

# Services

Do not create.

---

# Commands

Do not create.

---

# Queries

Do not create.

---

# Factory

Create FactoryBot factory.

Use realistic fake data.

---

# Tests

Create:

Model spec

Validation tests

Factory tests

Normalization tests

Enum tests

UUID tests

All tests must pass.

---

# Code Quality

Follow Rubocop.

Follow project standards.

No warnings.

No duplicated code.

---

# Out of Scope

Do NOT implement:

Authentication

Organizations

Organization Memberships

Roles

Permissions

JWT

Sessions

Controllers

Routes

Business Profile

Registration

Login

Anything outside the User identity.

---

# Deliverables

User migration

User model

Factory

UUID

Indexes

Validation

Normalization

Tests

---

# Acceptance Criteria

✓ Migration succeeds

✓ UUID primary key works

✓ User model loads

✓ Email is normalized

✓ Validation passes

✓ Factory passes

✓ Tests pass

✓ Rubocop passes

✓ Brakeman passes

Stop immediately after completing this task.

Do not continue into AUTH-003.

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