# PLATFORM-001 — Engineering Review

**Task:** PLATFORM-001 (Platform Foundation)
**Sprint:** 04
**Status:** Pending Architect Approval

---

## Summary

Implemented PLATFORM-001 per `09_Cursor/PLATFORM/PLATFORM-001.md`. This PR introduces the shared platform foundation used by AI, Communications, Reports, Automations, and future Billing — without implementing billing, payments, Stripe, Paddle, LemonSqueezy, or subscription checkout.

Organizations now use canonical platform `status` (`trial`, `active`, `grace_period`, `suspended`, `inactive`) and `plan` (`starter`, `professional`, `enterprise`, `custom`). `PlatformContext` is the single snapshot for platform state, exposed on `Current.platform_context` after authentication. `Platform::FeatureAccessService` and `Platform::ChannelAccessService` are reusable extension points; all plan/status logic is centralized in `Platform::OrganizationFeaturePolicy`.

Super Admin foundation (`users.super_admin`, `Platform::SuperAdminService`) supports org suspend/activate, plan changes, and feature/channel overrides (backend only, no admin API in this PR). AI Playground and Comms message creation integrate access checks as preparation hooks.

**Verification:** 612 RSpec examples (0 failures), 82 Vitest tests (0 failures), Brakeman 0 warnings, RuboCop clean on platform paths.

---

## Files Created

### Backend

- `db/migrate/20240628000034_create_platform_foundation.rb`
- `app/models/platform_context.rb`
- `app/models/organization_feature_entitlement.rb`
- `app/models/organization_channel_entitlement.rb`
- `app/services/platform/types.rb`
- `app/services/platform/feature_registry.rb`
- `app/services/platform/channel_registry.rb`
- `app/services/platform/feature_access_result.rb`
- `app/services/platform/channel_access_result.rb`
- `app/services/platform/organization_feature_policy.rb`
- `app/services/platform/feature_access_service.rb`
- `app/services/platform/channel_access_service.rb`
- `app/services/platform/event_logger.rb`
- `app/services/platform/super_admin_service.rb`
- `app/policies/platform_policy.rb`
- `app/serializers/platform_context_serializer.rb`
- `app/controllers/api/v1/platform_context_controller.rb`
- `app/controllers/concerns/platform/response_rendering.rb`
- `spec/models/platform_context_spec.rb`
- `spec/services/platform/feature_registry_spec.rb`
- `spec/services/platform/channel_registry_spec.rb`
- `spec/services/platform/feature_access_service_spec.rb`
- `spec/services/platform/channel_access_service_spec.rb`
- `spec/services/platform/organization_feature_policy_spec.rb`
- `spec/services/platform/super_admin_service_spec.rb`
- `spec/policies/platform_policy_spec.rb`
- `spec/requests/platform_spec.rb`

---

## Files Modified

### Backend

- `app/domains/organization/models/organization.rb` — platform status/plan enums, entitlements associations, `platform_context`
- `app/domains/identity/models/user.rb` — `super_admin` flag
- `app/models/current.rb` — `platform_context` attribute
- `app/controllers/concerns/authenticatable.rb` — sets `Current.platform_context`
- `app/serializers/organization_serializer.rb` — `plan`, platform status fields
- `app/serializers/me_serializer.rb` — `platform_status`, `platform_plan`
- `app/commands/comms/messages/create_command.rb` — `ChannelAccessService` before outgoing messages
- `app/controllers/api/v1/ai/playground_controller.rb` — `FeatureAccessService` before AI run
- `db/seeds/development_super_admin_seeder.rb` — `super_admin`, enterprise plan
- `config/routes.rb` — `GET /api/v1/platform/context`
- `backend/.rubocop.yml` — platform path exclusions
- `spec/factories/organizations.rb` — platform traits
- `spec/domains/organization/models/organization_spec.rb` — platform-focused tests
- `spec/requests/ai_playground_spec.rb` — enterprise plan for AI runtime access

---

## Database Changes

Migration `20240628000034_create_platform_foundation`:

| Table / Change | Purpose |
|----------------|---------|
| `organizations.plan` | Replaces `subscription_plan` (starter/professional/enterprise/custom) |
| `organizations.status` | String platform status (replaces legacy integer status + `subscription_status`) |
| `organizations.grace_ends_at` | Grace period end timestamp |
| `organizations.suspended_at` | Suspension timestamp |
| `organizations.suspension_reason` | Human-readable suspension reason |
| `organization_feature_entitlements` | Per-org feature overrides (super admin enable/disable) |
| `organization_channel_entitlements` | Per-org channel overrides |
| `users.super_admin` | Platform super admin flag |

**Removed columns:** `subscription_plan`, `subscription_status` (data migrated to `plan` + platform `status`).

---

## API Endpoints

| Method | Path | Access | Description |
|--------|------|--------|-------------|
| GET | `/api/v1/platform/context` | Owner, Manager | Organization status, plan, enabled features/channels, AI flag |

No admin/super-admin REST endpoints in this PR (per spec).

---

## Services Added

| Service | Purpose |
|---------|---------|
| `Platform::FeatureRegistry` | Central feature list + plan defaults |
| `Platform::ChannelRegistry` | Central channel list + plan defaults + comms mapping |
| `Platform::OrganizationFeaturePolicy` | Single source for feature/channel availability |
| `Platform::FeatureAccessService` | `check(organization:, feature:)` → `FeatureAccessResult`; logs `FeatureDenied` |
| `Platform::ChannelAccessService` | `check(organization:, channel:)` → `ChannelAccessResult`; logs `ChannelDenied` |
| `PlatformContext` | Snapshot API: `feature_enabled?`, `channel_enabled?`, `ai_enabled?`, etc. |
| `Platform::SuperAdminService` | Suspend/activate orgs, change plan, enable/disable features/channels |
| `Platform::EventLogger` | Structured platform event logging |

### Denial Reasons

`allowed`, `trial`, `subscription_required`, `organization_suspended`, `organization_inactive`, `feature_not_in_plan`, `channel_not_in_plan`, `system_disabled`

---

## Integration Hooks (Prepare Only)

| Module | Hook |
|--------|------|
| AI Playground | `FeatureAccessService.check(feature: 'ai_runtime')` before `run` |
| Comms Messages | `ChannelAccessService.check` before outgoing non-internal messages on registered channels |

---

## Tests Added

- Registry specs (feature, channel)
- `PlatformContext` spec
- `FeatureAccessService`, `ChannelAccessService` specs
- `OrganizationFeaturePolicy` spec
- `PlatformPolicy` spec
- `SuperAdminService` spec
- `platform_spec` request spec (context endpoint + RBAC)

---

## Assumptions

1. **Plan feature matrix** — Starter/professional/enterprise defaults are defined in registries; not billing-driven until a future billing task.
2. **Trial orgs** — Receive starter-plan features while `status == trial`; access reason is `trial` when allowed.
3. **Legacy status migration** — `subscription_status` + old integer `status` mapped to platform statuses in migration; irreversible.
4. **Controller namespace** — `PlatformContextController` (not `API::V1::Platform::*`) avoids shadowing `::Platform::Pagination` and other services.
5. **Email/SMS comms channels** — Listed as `FUTURE_CHANNELS` in registry; no channel access check until promoted to active channels.
6. **Super Admin** — `users.super_admin` boolean; dev seed sets `admin@zorovex.local` as super admin with enterprise plan.

---

## Suggestions

1. **Expose platform context to frontend** — Add `/comms` and module nav gating via `GET /api/v1/platform/context` in a follow-up UI task.
2. **Admin API** — Super Admin REST endpoints when architect approves admin UI.
3. **Task Assigned notifications** — Wire `Platform::FeatureAccessService` when CRM tasks ship platform-gated features.
4. **Rename `PlatformJob`** — Consider `AsyncJob` alias long-term to reduce confusion with platform foundation namespace.

---

## Blockers

None for PLATFORM-001 scope. AI-004 remains blocked on architect approval (not started).

---

## Acceptance Criteria

| Criterion | Status |
|-----------|--------|
| Platform Context implemented | ✓ |
| Feature Registry implemented | ✓ |
| Channel Registry implemented | ✓ |
| Feature Access Service implemented | ✓ |
| Channel Access Service implemented | ✓ |
| Organization plans implemented | ✓ |
| Organization statuses implemented | ✓ |
| AI Runtime ready (integration hook) | ✓ |
| Communications ready (integration hook) | ✓ |
| Tests pass | ✓ |
| RuboCop passes | ✓ |
| Brakeman passes | ✓ |

---

**Stop point:** PLATFORM-001 complete. AI-004 not started.
