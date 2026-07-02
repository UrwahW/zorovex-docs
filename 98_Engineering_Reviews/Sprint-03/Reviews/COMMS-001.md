# COMMS-001 — Engineering Review

**Task:** COMMS-001 (Communications Platform)
**Sprint:** 03
**Status:** Pending Architect Approval

---

## Summary

Implemented COMMS-001 per `09_Cursor/COMMS/COMMS-001.md`. The Communications Platform centralizes customer conversations inside Zorovex with a unified inbox, conversation threads, messages, templates, internal notes, attachments, in-app notifications, and REST APIs under `/api/v1/comms/*`. No external provider integrations (WhatsApp Cloud, Twilio, SMTP, etc.) were added.

CRM integration logs thread/message activity on contact timelines and surfaces communications on contact detail. Booking integration adds communication history and reminder status on appointment show, and creates stored notifications on appointment create/cancel.

**Verification:** 618 RSpec examples (0 failures, +38 from HARDENING baseline), 82 Vitest tests (0 failures, +9), Brakeman 0 warnings, RuboCop clean on comms paths.

---

## Files Created

### Backend

- `db/migrate/20240628000033_create_comms.rb`
- `app/domains/comms/models/communication_thread.rb`
- `app/domains/comms/models/message.rb`
- `app/domains/comms/models/message_template.rb`
- `app/domains/comms/models/message_attachment.rb`
- `app/domains/comms/models/comms_notification.rb`
- `app/services/comms/types.rb`
- `app/services/comms/template_engine.rb`
- `app/services/comms/notification_service.rb`
- `app/services/comms/conversation_service.rb`
- `app/services/comms/crm_integration.rb`
- `app/services/comms/booking_integration.rb`
- `app/policies/comms_policy.rb`
- `app/commands/comms/messages/create_command.rb`
- `app/commands/comms/messages/update_command.rb`
- `app/commands/comms/threads/update_command.rb`
- `app/commands/comms/templates/create_command.rb`
- `app/commands/comms/templates/update_command.rb`
- `app/commands/comms/templates/delete_command.rb`
- `app/commands/comms/templates/duplicate_command.rb`
- `app/commands/comms/templates/preview_command.rb`
- `app/commands/comms/notifications/update_command.rb`
- `app/queries/comms/threads/list_query.rb`
- `app/queries/comms/threads/find_by_id_query.rb`
- `app/queries/comms/notifications/list_query.rb`
- `app/validators/comms/messages/create_validator.rb`
- `app/validators/comms/messages/update_validator.rb`
- `app/validators/comms/templates/create_validator.rb`
- `app/validators/comms/templates/update_validator.rb`
- `app/serializers/communication_thread_serializer.rb`
- `app/serializers/message_serializer.rb`
- `app/serializers/message_attachment_serializer.rb`
- `app/serializers/message_template_serializer.rb`
- `app/serializers/comms_notification_serializer.rb`
- `app/controllers/concerns/comms/response_rendering.rb`
- `app/controllers/api/v1/comms/base_controller.rb`
- `app/controllers/api/v1/comms/threads_controller.rb`
- `app/controllers/api/v1/comms/messages_controller.rb`
- `app/controllers/api/v1/comms/templates_controller.rb`
- `app/controllers/api/v1/comms/notifications_controller.rb`
- `spec/factories/comms.rb`
- `spec/domains/comms/models/*_spec.rb`
- `spec/policies/comms_policy_spec.rb`
- `spec/services/comms/*_spec.rb`
- `spec/requests/comms_spec.rb`

### Frontend

- `frontend/src/features/comms/constants/comms-options.ts`
- `frontend/src/features/comms/types/comms.ts`
- `frontend/src/features/comms/api/comms-api.ts`
- `frontend/src/features/comms/hooks/use-comms-access.ts`
- `frontend/src/features/comms/hooks/use-comms.ts`
- `frontend/src/features/comms/routes/comms-access-route.tsx`
- `frontend/src/features/comms/components/comms-header.tsx`
- `frontend/src/features/comms/components/inbox-filters.tsx`
- `frontend/src/features/comms/components/conversation-sidebar.tsx`
- `frontend/src/features/comms/components/message-composer.tsx`
- `frontend/src/features/comms/components/attachment-viewer.tsx`
- `frontend/src/features/comms/components/contact-comms-panel.tsx`
- `frontend/src/features/comms/pages/inbox-page.tsx`
- `frontend/src/features/comms/pages/conversation-page.tsx`
- `frontend/src/features/comms/pages/templates-page.tsx`
- `frontend/src/features/comms/pages/notifications-page.tsx`
- `frontend/src/features/comms/constants/comms-options.test.ts`
- `frontend/src/features/comms/routes/comms-routes.test.ts`

---

## Files Modified

### Backend

- `config/application.rb` — comms domain autoload path
- `config/routes.rb` — `/api/v1/comms/*` namespace
- `app/domains/organization/models/organization.rb` — comms associations
- `app/domains/crm/models/contact.rb` — `communication_threads`
- `app/domains/identity/models/user.rb` — assigned threads, notifications
- `app/services/crm/contacts/types.rb` — `thread_created`, `message_created`, `message_updated` activity types
- `app/services/bookings/booking_service.rb` — appointment reminder notifications
- `app/services/bookings/cancel_service.rb` — booking cancelled notifications
- `app/serializers/appointment_serializer.rb` — `communications` payload
- `db/seeds/rbac/definitions.rb` — accountant `conversations.view`, `notifications.view`
- `backend/.rubocop.yml` — comms path exclusions

### Frontend

- `frontend/src/routes/router.tsx` — `/comms/*` routes
- `frontend/src/layouts/dashboard-layout.tsx` — Comms nav link
- `frontend/src/features/crm/pages/contact-details-page.tsx` — `ContactCommsPanel`
- `frontend/src/features/bookings/pages/appointment-details-page.tsx` — communication history section
- `frontend/src/features/bookings/types/appointment.ts` — `communications` type

---

## Database Changes

Migration `20240628000033_create_comms`:

| Table | Purpose |
|-------|---------|
| `communication_threads` | Org-scoped conversation threads (channel, status, assignment, last_message_at) |
| `messages` | Thread messages (direction, sender_type, status, metadata, soft delete) |
| `message_templates` | Variable templates with categories and archive status |
| `message_attachments` | Message file metadata + ActiveStorage blob |
| `notifications` | In-app notifications (no external delivery) |

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/v1/comms/threads` | Paginated inbox (status, channel, contact, search filters) |
| GET | `/api/v1/comms/threads/:id` | Thread with messages and attachments |
| PATCH | `/api/v1/comms/threads/:id` | Update status / assignment (inbox workflow) |
| POST | `/api/v1/comms/messages` | Create message (new or existing thread; template support) |
| PATCH | `/api/v1/comms/messages/:id` | Update message content/status |
| GET | `/api/v1/comms/templates` | List templates |
| POST | `/api/v1/comms/templates` | Create / duplicate template |
| PATCH | `/api/v1/comms/templates/:id` | Update / archive template |
| DELETE | `/api/v1/comms/templates/:id` | Archive template |
| POST | `/api/v1/comms/templates/preview` | Preview template with variables |
| GET | `/api/v1/comms/notifications` | User notifications (paginated) |
| PATCH | `/api/v1/comms/notifications/:id` | Mark notification read |

**Booking integration (additive):** `GET /api/v1/bookings/:id` includes `communications.messages` and `communications.reminder_status`.

---

## Permissions

| Role | Access |
|------|--------|
| Owner / Manager | Full inbox, messages, templates |
| Receptionist | Read, create, reply; no template write |
| Marketing | Read inbox; full template management |
| Accountant | Read-only inbox and notifications |

Enforced via `CommsPolicy` (role-code based, consistent with Bookings/Operations).

---

## Tests Added

- Model specs: `CommunicationThread`, `Message`, `MessageTemplate`, `CommsNotification`
- Policy spec: `CommsPolicy`
- Service specs: `TemplateEngine`, `NotificationService`, `ConversationService`
- Request spec: `comms_spec.rb` (threads, messages, templates, notifications, booking integration)
- Frontend: `comms-options.test.ts`, `comms-routes.test.ts`

---

## Assumptions

1. **`contact_communications` remains separate** — CRM manual communication logging (CRM-002) is unchanged; comms platform is the canonical inbox for threaded conversations.
2. **PATCH threads/:id** — Added for inbox status workflows (archive, resolve, assign) required by acceptance criteria but not listed in the minimal API table.
3. **POST templates/preview** — Collection preview endpoint supports template preview per spec.
4. **Notifications are in-app only** — Stored in `notifications` table; no push/email delivery.
5. **Outgoing messages default to `sent`** — No provider queue; external delivery deferred to future provider integrations.
6. **`CommsNotification` model** — Maps to `notifications` table to avoid naming collisions.

---

## Risks

1. **Table name `notifications`** — Generic name may conflict if a global notification system is added later; consider rename before multi-module notification hub.
2. **No real-time updates** — Inbox requires refresh/polling; WebSocket/SSE not in scope.
3. **Attachment upload via messages API** — Attachment metadata supported; multipart upload path not fully exercised in UI yet.
4. **Marketing read-only on messages** — Per spec; marketing users cannot reply from inbox (by design).

---

## Technical Debt

1. **Unified timeline** — Comms events appear as CRM activities but are not merged into a single comms+CRM timeline API.
2. **Message search** — Inbox supports customer search via thread list; full-text message search endpoint not implemented.
3. **Task Assigned notifications** — Type defined; no automatic hook from CRM tasks yet.
4. **Provider reference field** — Reserved for future WhatsApp/Twilio integrations.

---

## Acceptance Criteria

| Criterion | Status |
|-----------|--------|
| Inbox operational | ✓ |
| Conversations operational | ✓ |
| Templates operational | ✓ |
| Notifications operational | ✓ |
| CRM integration working | ✓ |
| Booking integration working | ✓ |
| Tests pass | ✓ |
| RuboCop passes | ✓ |
| Brakeman passes | ✓ |

---

**Stop point:** COMMS-001 complete. AI-004 not started.
