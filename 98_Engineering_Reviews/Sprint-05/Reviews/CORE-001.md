# CORE-001 — Engineering Review

**Task:** CORE-001 (Organization Platform)
**Sprint:** Sprint 05
**Status:** Pending Architect Approval
**Depends On:** AUTH-001, PLATFORM-001, PLATFORM-002

---

## Summary

Implemented the Organization Platform as the canonical source of truth for business identity separate from operational configuration. Unified APIs aggregate organization shell, profile, branding, localization, metadata, subscription, feature flags, integrations, and health. Built on existing `Organization`, `BusinessProfile`, and platform entitlement infrastructure. Registration now assigns `owner_id` and seeds subscription records. Frontend dashboard at `/organization`.

---

## Services Added

| Service | Purpose |
|---------|---------|
| `Organizations::OrganizationPlatformService` | Aggregated show/update |
| `Organizations::OrganizationLifecycleService` | Activate, suspend, archive, restore, soft delete, ownership transfer |
| `Organizations::BrandingService` | Brand colors and email branding |
| `Organizations::LocalizationService` | Timezone, language, currency, formats |
| `Organizations::FeatureFlagService` | Per-org feature overrides |
| `Organizations::SubscriptionService` | Plan, billing cycle, seats, usage limits |
| `Organizations::OrganizationHealthService` | Usage and health snapshot |
| `Organizations::IntegrationsService` | Provider catalog (config references only) |

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/v1/organization` | Full organization platform payload |
| PATCH | `/api/v1/organization` | Update profile, branding, localization, metadata |
| GET | `/api/v1/organization/subscription` | Subscription details |
| GET | `/api/v1/organization/features` | Feature flags |
| PATCH | `/api/v1/organization/features` | Update feature overrides (owner) |
| GET | `/api/v1/organization/integrations` | Integration provider catalog |

---

## Domain Events

| Event | Trigger |
|-------|---------|
| `OrganizationUpdated` | Profile/platform update |
| `OrganizationActivated` | Lifecycle activate/restore |
| `OrganizationSuspended` | Lifecycle suspend |
| `OrganizationArchived` | Lifecycle archive/delete |
| `FeatureFlagChanged` | Feature override update |
| `LocalizationUpdated` | Localization change |
| `SubscriptionChanged` | Via plan sync (future billing hook) |
| `BrandingUpdated` | Logged structurally |

---

## Database

| Table / Change | Purpose |
|----------------|---------|
| `organizations` | Added `public_name`, `internal_name`, `owner_id`, `archived_at`, `deleted_at` |
| `business_profiles` | Added support contact, registration/tax fields |
| `organization_brandings` | Colors, dark logo, favicon, email branding |
| `organization_metadata` | Industry, size, tags, internal notes |
| `organization_preferences` | Date/time/number formats, week start |
| `organization_subscriptions` | Billing cycle, seats, storage, usage limits |
| `organization_integrations` | Provider connection references |

Migration: `20240628000047_create_organization_platform.rb`

---

## Frontend

| Route | Feature |
|-------|---------|
| `/organization` | Profile, branding, localization, subscription, features, health, integrations |

Business Setup wizard remains for onboarding; Organization dashboard is the post-setup settings surface.

---

## Permissions

| Role | Access |
|------|--------|
| Owner | Full update + feature flags |
| Manager | Profile update |
| Marketing | Read + branding view |
| Accountant | Subscription read |
| Receptionist | Read |

---

## Tests

- `spec/requests/organization_spec.rb` (5 examples)
- `spec/services/organizations/feature_flag_service_spec.rb` (1 example)

All 6 organization specs pass.

---

## Assumptions

- Identity fields remain on `BusinessProfile`; platform tables hold branding/metadata/preferences extensions.
- Subscription is plan/status tracking without Stripe integration (billing self-service deferred).
- Integrations store configuration references only — no provider OAuth logic.
- Lifecycle service exists for admin/internal use; not all actions exposed via public API yet.

---

## Risks

- Dual paths for profile edits (business-setup APIs vs organization API) until consolidated.
- Feature flag `CORE_FEATURES` must stay aligned with `Platform::Types::FEATURES`.

---

## Technical Debt

- Stripe/billing integration for subscription management.
- Expose lifecycle APIs for super-admin/owner self-service.
- Consolidate business-setup and organization settings into single UX.
- Wire frontend nav gating to platform feature entitlements.

---

## Acceptance Criteria

- [x] Organization Platform operational
- [x] Branding operational
- [x] Localization operational
- [x] Subscription operational
- [x] Feature Flags operational
- [x] APIs operational
- [x] Tests pass
- [ ] RuboCop / Brakeman — not run full suite in this session
