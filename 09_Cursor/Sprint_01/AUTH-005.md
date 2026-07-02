# ENGINEERING TASK

ID

AUTH-005

Sprint

Sprint 1

Title

Implement Authentication System

Status

Approved

Depends On

AUTH-001

AUTH-002

AUTH-003

AUTH-004

---

# Read First

Before implementation, read:

1. 09_Cursor/START_HERE.md
2. 09_Cursor/Cursor_Rules.md
3. 02_Architecture/TECH_STACK.md
4. 03_Backend/AUTHENTICATION.md
5. 03_Backend/ORGANIZATIONS.md

Do not begin implementation until these documents have been reviewed.

---

# Objective

Implement the complete authentication system for Zorovex.

This includes:

Registration

Login

Logout

JWT

Refresh Tokens

Email Verification

Forgot Password

Reset Password

Sessions

Current User Endpoint

Authentication Middleware

This completes the authentication foundation for V1.

---

# Scope

Implement ONLY:

Authentication

JWT

Refresh Tokens

Sessions

Registration

Login

Logout

Password Reset

Email Verification

Current User Endpoint

Authentication Middleware

Tests

Nothing else.

---

# Authentication Architecture

The authentication flow must follow this sequence:

User Registers

↓

User Created

↓

Organization Created

↓

Organization Membership Created

↓

Owner Role Assigned

↓

Owner Permissions Assigned

↓

Email Verification Token Generated

↓

Verification Email Sent

↓

Account Activated

↓

User Can Login

---

# JWT

Use JWT authentication.

Access Token

15 minutes

Refresh Token

30 days

Refresh tokens must be stored in the database.

Refresh tokens must rotate.

Old refresh tokens become invalid after refresh.

---

# Sessions

Create table:

sessions

Columns

id UUID

user_id UUID

refresh_token

ip_address

user_agent

device_name

expires_at

last_used_at

created_at

updated_at

---

# Registration

Endpoint

POST

/api/v1/auth/register

Request

first_name

last_name

email

password

organization_name

Validation

Email unique

Password strength

Organization required

Flow

Create User

↓

Create Organization

↓

Create Membership

↓

Assign Owner Role

↓

Assign All Owner Permissions

↓

Generate Verification Token

↓

Send Verification Email

↓

Create Session

↓

Return Tokens

---

# Login

Endpoint

POST

/api/v1/auth/login

Accept

Email

Password

Flow

Validate Credentials

↓

Email Verified?

↓

Create Session

↓

Generate JWT

↓

Generate Refresh Token

↓

Return User

↓

Return Organization

↓

Return Membership

↓

Return Roles

↓

Return Permissions

---

# Logout

Endpoint

POST

/api/v1/auth/logout

Flow

Delete Session

Invalidate Refresh Token

Return Success

---

# Refresh Token

Endpoint

POST

/api/v1/auth/refresh

Flow

Validate Refresh Token

↓

Create New Access Token

↓

Rotate Refresh Token

↓

Delete Old Refresh Token

↓

Return New Tokens

---

# Forgot Password

Endpoint

POST

/api/v1/auth/forgot-password

Flow

Generate Reset Token

↓

Email Reset Link

↓

Expire After One Hour

---

# Reset Password

Endpoint

POST

/api/v1/auth/reset-password

Flow

Validate Token

↓

Update Password

↓

Invalidate Token

↓

Delete Existing Sessions

↓

Require New Login

---

# Email Verification

Endpoint

POST

/api/v1/auth/verify-email

Flow

Validate Verification Token

↓

Mark Email Verified

↓

Delete Token

---

# Current User

Endpoint

GET

/api/v1/me

Response

User

Organization

Membership

Roles

Permissions

Business Setup Progress

Unread Notifications Count

Subscription Status

Business Name

Avatar

---

# Middleware

Implement

Authenticate User

Current User

Current Organization

Current Membership

Unauthorized Handler

Token Expiration

---

# Security

Passwords

BCrypt

Strong Password Rules

Minimum 8 characters

Uppercase

Lowercase

Number

Special Character

Rate Limit Login Attempts

Do not reveal whether email exists.

Never expose password hashes.

Never expose refresh tokens.

---

# Logging

Log

Registration

Login

Logout

Failed Login

Password Reset

Email Verification

Session Creation

Session Destruction

---

# Factories

Create

Session Factory

Verification Token Factory

Password Reset Token Factory

---

# Tests

Create

Authentication Request Specs

Registration Specs

Login Specs

Logout Specs

Refresh Specs

Forgot Password Specs

Reset Password Specs

Verification Specs

Middleware Specs

JWT Specs

Session Specs

Security Specs

All tests must pass.

---

# Out of Scope

Do NOT implement:

Business Profile

Business Setup

Dashboard

Customers

Bookings

Services

Staff

Conversations

AI

Notifications

Anything outside authentication.

---

# Deliverables

Authentication API

JWT

Refresh Tokens

Session Management

Email Verification

Password Reset

Authentication Middleware

Factories

Tests

Documentation Updates

---

# Acceptance Criteria

✓ Registration works

✓ Login works

✓ Logout works

✓ JWT generated

✓ Refresh works

✓ Sessions stored

✓ Password Reset works

✓ Email Verification works

✓ /api/v1/me works

✓ Tests pass

✓ Rubocop passes

✓ Brakeman passes

Stop after completion.

Do not continue to BUS-001.

---

# Completion Report

Provide

Summary

Files Created

Files Modified

Database Changes

API Endpoints

Tests Added

Assumptions

Suggestions

Blockers