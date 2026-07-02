# BUSINESS PROFILE

Version: 1.0

Status: Approved

Sprint: 1

---

# Purpose

The Business Profile represents the public and operational identity of a business using Zorovex.

Every Organization owns exactly one Business Profile in Version 1.

Future versions will support multiple branches through Branch Profiles.

---

# Responsibilities

The Business Profile stores information required by:

- AI Receptionist
- CRM
- Booking System
- Google Calendar
- WhatsApp
- Facebook
- Instagram
- Voice Agent
- Marketing
- Customer Communication

---

# Database

Table

business_profiles

Columns

id UUID

organization_id UUID

business_name string

legal_name string

industry_id UUID

description text

phone string

email string

website string

logo_path string

cover_image_path string

currency string

timezone string

language string

country string

city string

address text

postal_code string

google_maps_url text

facebook_url text

instagram_url text

linkedin_url text

youtube_url text

status integer

created_at

updated_at

---

# Associations

BusinessProfile

belongs_to Organization

belongs_to Industry

---

# Status

draft

active

disabled

archived

---

# Business Rules

Each Organization has exactly one Business Profile.

Business Name is required.

Industry is required.

Timezone is required.

Currency is required.

Country is required.

Logo is optional.

Cover image is optional.

---

# Validation

Business Name

Minimum 2 characters

Maximum 150 characters

Website

Must be valid URL

Email

Valid email

Phone

International format

Country

ISO Country Code

Currency

ISO Currency Code

Timezone

IANA Timezone

---

# File Uploads

Support:

Logo

PNG

JPEG

SVG

Maximum 5 MB

Cover Image

PNG

JPEG

Maximum 10 MB

Files stored using Active Storage.

---

# Audit

Every update creates an Audit Log.

Store:

User

Timestamp

Changed Fields

Previous Values

New Values

---

# Events

BusinessProfileCreated

BusinessProfileUpdated

BusinessProfileActivated

BusinessProfileArchived

---

# API

GET /api/v1/business-profile

POST /api/v1/business-profile

PATCH /api/v1/business-profile

DELETE /api/v1/business-profile

DELETE performs a soft delete.

---

# Response

Always follow API standards.

{
  "success": true,
  "data": {}
}

---

# Security

Only authenticated users.

Only Organization Members.

Only Owner and Manager can update profile.

Receptionists have read-only access.

---

# Out of Scope

Business Setup Wizard

Working Hours

Services

Staff

Knowledge

Channels

These belong to later specifications.