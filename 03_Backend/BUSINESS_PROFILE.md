# Business Profile

> Status: Approved

The business profile stores operational identity and contact details for an organization.

One organization has exactly one business profile.

The profile is created when the organization is created and is completed through the Business Setup Wizard.

---

# Purpose

The business profile answers:

- What is this business called?
- What type of business is it?
- How can customers contact it?
- What timezone does it operate in?
- Has onboarding been completed?

The profile is used by:

- Dashboard header and branding
- AI context (Business Brain)
- Customer-facing channels (WhatsApp, email, booking pages)
- `/api/v1/me` setup progress checks

---

# Domain Rules

- Every `organization` has exactly one `business_profile`
- `business_profile.organization_id` is unique
- Profile is scoped to the current organization — no cross-tenant access
- Profile is created automatically when an organization is created
- Profile starts incomplete until the setup wizard finishes
- Only `owner` and `admin` roles may update the profile
- `staff` may read the profile
- Soft delete is not used — profile is deleted only when the organization is deleted

---

# Relationship

```
Organization (1) ──── (1) BusinessProfile
```

| Entity | Relationship |
|--------|--------------|
| Organization | Parent. Created at registration. |
| BusinessProfile | Child. Created immediately after organization creation. |
| BusinessType | Reference value on profile (`business_type`). See `01_Product/BUSINESS_TYPES.md`. |

---

# Database

Table: `business_profiles`

| Column | Type | Required | Notes |
|--------|------|----------|-------|
| id | UUID | yes | Primary key |
| organization_id | UUID | yes | FK → organizations, unique |
| display_name | string | no | Public business name |
| legal_name | string | no | Registered legal name |
| business_type | string | no | e.g. `salon`, `clinic`, `agency` |
| timezone | string | no | IANA timezone, e.g. `Europe/London` |
| email | string | no | Public contact email |
| phone | string | no | Public contact phone |
| website | string | no | URL |
| address_line_1 | string | no | |
| address_line_2 | string | no | |
| city | string | no | |
| state | string | no | |
| postal_code | string | no | |
| country | string | no | ISO 3166-1 alpha-2 |
| logo_url | text | no | Active Storage or CDN URL |
| setup_step | integer | yes | Current wizard step, default `0` |
| setup_completed_at | datetime | no | Set when wizard completes |
| created_at | datetime | yes | |
| updated_at | datetime | yes | |

## Indexes

- Unique index on `organization_id`
- Index on `business_type`
- Index on `setup_completed_at`

## Foreign Keys

- `organization_id` → `organizations.id` (on delete: cascade)

---

# Setup Status

Profile completion is derived from `setup_completed_at` and `setup_step`.

| State | Condition |
|-------|-----------|
| `not_started` | `setup_step` = 0 and `setup_completed_at` is null |
| `in_progress` | `setup_step` > 0 and `setup_completed_at` is null |
| `completed` | `setup_completed_at` is present |

## Required Fields for Completion

All of the following must be present before `setup_completed_at` is set:

- `display_name`
- `business_type`
- `timezone`
- `email` or `phone` (at least one contact method)

Wizard step mapping is defined in `03_Backend/BUSINESS_SETUP.md`.

---

# API

Base path: `/api/v1/business-profile`

All endpoints require authentication.

Organization context is resolved from the current session — never from request body.

## Response Envelope

Success:

```json
{
  "success": true,
  "data": {}
}
```

Failure:

```json
{
  "success": false,
  "message": "...",
  "errors": []
}
```

---

## GET /api/v1/business-profile

Returns the business profile for the current organization.

**Authorization:** `owner`, `admin`, `staff`

**Response `data`:**

```json
{
  "id": "uuid",
  "organization_id": "uuid",
  "display_name": "Acme Salon",
  "legal_name": null,
  "business_type": "salon",
  "timezone": "Europe/London",
  "email": "hello@acme.com",
  "phone": "+441234567890",
  "website": null,
  "address_line_1": null,
  "address_line_2": null,
  "city": null,
  "state": null,
  "postal_code": null,
  "country": "GB",
  "logo_url": null,
  "setup_step": 2,
  "setup_completed_at": null,
  "setup_status": "in_progress",
  "created_at": "2026-01-01T00:00:00Z",
  "updated_at": "2026-01-01T00:00:00Z"
}
```

---

## PATCH /api/v1/business-profile

Updates profile fields for the current organization.

**Authorization:** `owner`, `admin`

**Request body** (all fields optional):

```json
{
  "display_name": "Acme Salon",
  "legal_name": "Acme Salon Ltd",
  "business_type": "salon",
  "timezone": "Europe/London",
  "email": "hello@acme.com",
  "phone": "+441234567890",
  "website": "https://acme.com",
  "address_line_1": "1 High Street",
  "city": "London",
  "postal_code": "SW1A 1AA",
  "country": "GB",
  "setup_step": 3
}
```

**Validation:**

- `display_name` — max 255 characters
- `business_type` — must be a supported type from `01_Product/BUSINESS_TYPES.md`
- `timezone` — must be a valid IANA timezone
- `email` — valid email format
- `phone` — E.164 or normalized local format
- `website` — valid URL
- `country` — valid ISO 3166-1 alpha-2 code
- `setup_step` — integer ≥ 0

**Behavior:**

- Partial updates allowed
- Setting `setup_step` does not auto-complete the profile
- `setup_completed_at` is set only by the setup completion command (see `03_Backend/BUSINESS_SETUP.md`)

---

## POST /api/v1/business-profile/complete

Marks the business profile setup as complete.

**Authorization:** `owner`, `admin`

**Validation:**

- All required completion fields must be present
- Returns 422 with field errors if incomplete

**Response `data`:**

```json
{
  "setup_status": "completed",
  "setup_completed_at": "2026-01-01T00:00:00Z"
}
```

---

# Integration with /api/v1/me

`GET /api/v1/me` includes business profile summary fields:

```json
{
  "business_name": "Acme Salon",
  "business_setup_progress": {
    "setup_status": "in_progress",
    "setup_step": 2,
    "setup_completed_at": null
  }
}
```

`business_name` maps to `business_profiles.display_name`.

See `03_Backend/AUTHENTICATION.md`.

---

# Application Layer

Follow modular monolith conventions from `09_Cursor/Cursor_Rules.md`.

| Layer | Responsibility |
|-------|----------------|
| Controller | `Api::V1::BusinessProfileController` — auth, params, response |
| Command | `BusinessProfiles::UpdateCommand` |
| Command | `BusinessProfiles::CompleteSetupCommand` |
| Query | `BusinessProfiles::FindByOrganizationQuery` |
| Service | `BusinessProfiles::SetupStatusService` |
| Serializer | `BusinessProfileSerializer` |
| Policy | `BusinessProfilePolicy` |

Controllers must not contain business logic.

---

# Events

Emit domain events after successful writes:

| Event | When |
|-------|------|
| `business_profile.created` | Profile created with organization |
| `business_profile.updated` | Profile fields updated |
| `business_profile.setup_completed` | `setup_completed_at` set |

See `02_Architecture/EVENT_SYSTEM.md`.

---

# Logging

Log:

- Profile created
- Profile updated (organization_id, changed fields)
- Setup completed
- Setup completion rejected (missing fields)

---

# Tests

Required coverage:

- Factory for `business_profile`
- Model validations
- Unique `organization_id` constraint
- GET returns profile for current org
- PATCH updates allowed fields
- PATCH denied for `staff` role
- Cross-tenant access denied
- Complete endpoint sets `setup_completed_at` when valid
- Complete endpoint returns 422 when required fields missing
- Setup status transitions (`not_started` → `in_progress` → `completed`)

---

# Out of Scope (V1)

- Multiple locations per profile
- Profile versioning / audit history
- Public unauthenticated profile page
- Logo upload flow (URL field only in V1; upload via Active Storage in a later task)

---

# Related Docs

- [ORGANIZATIONS.md](ORGANIZATIONS.md) — parent entity
- [BUSINESS_SETUP.md](BUSINESS_SETUP.md) — onboarding wizard flow and steps
- [AUTHENTICATION.md](AUTHENTICATION.md) — `/api/v1/me` integration
- [API.md](API.md) — global API conventions
- [DATABASE.md](DATABASE.md) — schema index
- [BUSINESS_TYPES.md](../01_Product/BUSINESS_TYPES.md) — supported business types
- [BUSINESS_SETUP_UI.md](../04_Frontend/BUSINESS_SETUP_UI.md) — wizard UI
