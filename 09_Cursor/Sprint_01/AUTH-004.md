# ENGINEERING TASK

ID

AUTH-004

Sprint

Sprint 1

Title

Implement Role-Based Access Control (RBAC)

Status

Approved

Depends On

AUTH-002
AUTH-003

---

# Read First

Before implementation, read:

1. 09_Cursor/START_HERE.md
2. 09_Cursor/Cursor_Rules.md
3. 02_Architecture/TECH_STACK.md
4. 02_Architecture/CODING_STANDARDS.md
5. 03_Backend/AUTHENTICATION.md
6. 03_Backend/ORGANIZATIONS.md

Do not begin implementation until these documents have been reviewed.

---

# Objective

Implement the complete Role-Based Access Control (RBAC) foundation.

A User receives permissions through Roles.

Roles are assigned to Organization Memberships.

Permissions are assigned to Roles.

This system will be used by every feature inside Zorovex.

This architecture is LOCKED.

---

# Scope

Implement ONLY:

- Role model
- Permission model
- OrganizationMembershipRole model
- RolePermission model
- Associations
- Seed data
- Factories
- Tests

Do NOT implement middleware.

Do NOT implement JWT.

Do NOT implement authorization checks.

---

# Architecture

User

↓

OrganizationMembership

↓

OrganizationMembershipRole

↓

Role

↓

RolePermission

↓

Permission

This architecture must be followed exactly.

---

# Database

## roles

Columns

id

UUID Primary Key

organization_id UUID

name string

required

code string

required

unique per organization

description text

nullable

is_system boolean

default true

status integer

default active

created_at

updated_at

---

Indexes

organization_id

organization_id + code UNIQUE

---

## permissions

Columns

id

UUID Primary Key

code string

required

global unique

module string

required

name string

required

description text

status integer

default active

created_at

updated_at

---

Indexes

code UNIQUE

module

---

## role_permissions

Columns

id UUID

role_id UUID

permission_id UUID

created_at

updated_at

---

Indexes

role_id + permission_id UNIQUE

---

## organization_membership_roles

Columns

id UUID

organization_membership_id UUID

role_id UUID

created_at

updated_at

---

Indexes

organization_membership_id + role_id UNIQUE

---

# Associations

Organization

has_many Roles

Role

belongs_to Organization

has_many RolePermissions

has_many Permissions through RolePermissions

has_many OrganizationMembershipRoles

Permission

has_many RolePermissions

OrganizationMembership

has_many OrganizationMembershipRoles

has_many Roles through OrganizationMembershipRoles

---

# Role Codes

Seed these default system roles.

owner

manager

receptionist

marketing

accountant

These are system roles.

Businesses may create additional custom roles later.

---

# Permission Naming Convention

Every permission must follow:

module.action

Examples

customers.view

customers.create

customers.update

customers.delete

bookings.view

bookings.create

bookings.cancel

services.view

services.update

staff.view

staff.update

billing.view

billing.update

analytics.view

settings.update

ai.configure

knowledge.manage

conversation.reply

campaigns.send

---

# Permission Modules

customers

services

staff

bookings

calendar

knowledge

analytics

billing

settings

conversations

campaigns

ai

organization

notifications

---

# Seed Data

Create a seeder.

Owner receives every permission.

Manager receives operational permissions.

Receptionist receives customer-facing permissions.

Marketing receives campaigns, conversations and analytics.

Accountant receives billing and reports.

Do not hardcode permissions elsewhere.

Everything comes from the database.

---

# Business Rules

Permissions are organization-independent.

Roles are organization-specific.

Organizations may create custom roles.

System roles cannot be deleted.

System roles may be cloned.

Duplicate permission assignments are not allowed.

Duplicate role assignments are not allowed.

---

# Factories

Create:

Role Factory

Permission Factory

RolePermission Factory

OrganizationMembershipRole Factory

---

# Tests

Create:

Model tests

Association tests

Validation tests

Seeder tests

Unique constraint tests

Factory tests

Business rule tests

All tests must pass.

---

# Out of Scope

Do NOT implement:

Authentication

JWT

Policies

Authorization middleware

API endpoints

Frontend

Business Profile

Business Setup

Anything outside RBAC.

---

# Deliverables

Role model

Permission model

RolePermission model

OrganizationMembershipRole model

Database migrations

Seeders

Factories

Tests

Associations

---

# Acceptance Criteria

✓ Migrations succeed

✓ Seeders execute successfully

✓ Owner receives all permissions

✓ Duplicate assignments rejected

✓ Associations work correctly

✓ Tests pass

✓ Rubocop passes

✓ Brakeman passes

Stop after completion.

Do not continue to AUTH-005.

---

# Completion Report

Provide:

Summary

Files Created

Files Modified

Database Changes

Seed Data Created

Tests Added

Assumptions

Suggestions

Blockers