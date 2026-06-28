# BUSINESS BRAIN

**Version:** 1.0
**Status:** Approved

---

# Purpose

The Business Brain is the structured intelligence layer at the centre of Zorovex.

It is where a business stores everything its AI and staff need to know — policies, services, documents, deals, tone of voice, and operational rules — in one organised, searchable, versioned system.

The Business Brain is not a file dump. It is not a simple FAQ page. It is the living memory of the business.

Every AI interaction, recommendation, and customer-facing response draws from the Business Brain. When the business changes a price, updates a refund policy, or launches a Ramadan campaign, the Brain updates — and every connected module reflects that change.

---

# Vision

Every business on Zorovex should have a Brain that is as complete and current as its best-trained employee.

A salon owner uploads their price list once. A clinic adds aftercare instructions. An agency stores campaign briefs. From that point forward, the AI Receptionist answers accurately, the Booking Assistant quotes correctly, the Upselling Engine suggests relevant offers, and staff always have a single source of truth.

The Business Brain turns scattered documents, tribal knowledge, and informal rules into structured intelligence that scales across every channel and every future AI employee.

---

# Design Principles

The Business Brain must be:

**Structured** — Every item has a type, category, and purpose. Nothing is an anonymous upload in a folder.

**Searchable** — Owners, staff, and AI can find the right answer quickly by title, tag, category, or natural language.

**Reusable** — One policy, one price list, one deal — referenced everywhere it is needed. No duplication across modules.

**Versioned** — Changes are tracked. Previous versions remain available for audit and rollback.

**Auditable** — Every item has an owner, a last-updated timestamp, and a clear history of what changed and when.

**AI-friendly** — Content is structured so AI can retrieve, reason over, and cite the correct source — not guess.

**Future-ready** — Designed to support vector search, OCR, embeddings, and multilingual content as the platform evolves. These capabilities are planned; the Brain is built to accommodate them without redesign.

---

# Core Responsibilities

The Business Brain is responsible for:

1. **Storing** everything the business knows — from a one-line FAQ to a 40-page brochure
2. **Organising** knowledge by type, category, priority, visibility, and validity
3. **Governing** what AI can say, what customers can see, and what stays internal
4. **Powering** AI Receptionist, Voice Agent, Booking Assistant, Upselling Engine, and future AI Employees
5. **Enabling** CRM recommendations, customer guidance, and escalation decisions
6. **Preserving** version history so changes are traceable and reversible

The Business Brain does not replace the CRM, bookings, or conversations. It informs them.

---

# Why Business Brain Instead of Knowledge Base

A traditional knowledge base is a library of articles. Search, read, done.

Zorovex businesses need more than that.

| Knowledge Base | Business Brain |
|----------------|----------------|
| Static articles | Structured knowledge + documents + rules + behaviour |
| One audience | Visibility levels (customer, AI, staff, owner) |
| Always current or always wrong | Validity windows (permanent, seasonal, date-ranged) |
| Search by keyword | Search by keyword, tag, category, priority, and future semantic search |
| Used by help widgets | Powers AI Receptionist, Voice, Booking, Upselling, Escalation, and future AI Employees |
| No behaviour layer | Includes AI tone, greeting, forbidden topics, and escalation rules |
| Flat structure | Typed knowledge with categories, tags, and version history |

The Business Brain subsumes and extends what a knowledge base does. Businesses that previously thought in terms of "uploading documents" now think in terms of "training their Brain."

---

# Types of Brain Knowledge

Every item in the Business Brain belongs to a knowledge type. Types determine how the item is stored, displayed, searched, and consumed by AI.

---

## Structured Knowledge

Human-readable content written directly in Zorovex. Used for policies, FAQs, service descriptions, and operational notes.

Examples:

- "We require 24 hours notice for cancellations"
- "Our laser treatments are not suitable during pregnancy"
- "Parking is available behind the building"

Structured knowledge is the fastest to create and the easiest for AI to quote directly.

---

## Policies

Formal business rules that govern how the business operates and how AI should behave when those rules apply.

### Refund Rules

When refunds are offered, partial or full, and under what conditions.

*Example:* "Full refund if cancelled 48 hours before appointment. No refund within 24 hours."

### Cancellation Policies

Notice periods, fees, and exceptions for missed or late cancellations.

*Example:* "Cancellations within 12 hours incur a 50% charge."

### Pricing Rules

How prices are quoted, when discounts apply, and what is included in a listed price.

*Example:* "All colour services include a consultation. Balayage pricing starts from £120 and varies by hair length."

Policies are high-priority Brain items. AI must follow them before improvising.

---

## FAQs

Short question-and-answer pairs for common customer enquiries.

*Example:*

- **Q:** Do you accept walk-ins?
- **A:** We recommend booking in advance. Walk-ins are accepted subject to availability.

FAQs are customer-visible by default and optimised for fast retrieval.

---

## Services

Descriptions, inclusions, exclusions, duration, and pricing guidance for each service the business offers.

Linked conceptually to the Services module but stored in the Brain so AI can explain services in natural conversation.

*Example:* "Deep tissue massage — 60 minutes. Includes consultation and aftercare advice. Not suitable for recent injuries."

---

## Business Rules

Operational logic that AI and staff follow during conversations and workflows.

*Example:* "Never book more than two appointments for the same customer on the same day."

*Example:* "Always confirm patch test date before booking colour services for new clients."

Business rules differ from policies: policies are customer-facing commitments; business rules are internal operating instructions.

---

# Documents

Files uploaded by the business. The Brain indexes and references them so AI can surface the right document or extract answers from its contents.

Supported document types (planned and current):

| Format | Typical Use |
|--------|-------------|
| PDF | Price lists, brochures, policy documents, menus |
| DOCX | Internal guides, templates, letters |
| Excel | Price matrices, staff rosters, inventory lists |
| Images | Menus, before/after galleries, signage, logos |
| Menus | Restaurant and café service menus |
| Catalogues | Product and service catalogues |
| Brochures | Marketing and promotional brochures |
| Marketing Material | Flyers, social assets, campaign creative |

Documents are Brain items with attachments. The Brain tracks what each document is for, who can see it, and when it is valid — not just where the file lives.

---

# Deals

Time-bound or promotional offers that AI and the Upselling Engine can reference.

### Seasonal Campaigns

*Example:* Summer Glow Package — June to August. Includes facial, body scrub, and complimentary consultation.

### Holiday Promotions

*Example:* Eid Special — 20% off all bridal packages during the first week of Eid.

### Flash Deals

*Example:* Last-minute Tuesday slots — 30% off any available 2pm appointment, valid only on Tuesdays this month.

### Packages

Bundled services sold together at a set or discounted price.

*Example:* Wedding Package — trial, bridal day, and bridesmaid styling. From £850.

Deals support effective and expiry dates so AI never promotes an expired offer.

---

# AI Behaviour

The Business Brain includes a behaviour layer that defines how AI represents the business — separate from what it knows.

### Greeting

How AI opens a conversation.

*Example:* "Good afternoon! Welcome to Luxe Salon. How can I help you today?"

### Tone

The personality AI adopts.

*Example:* Warm, professional, concise. Never overly casual. Never use slang.

Aligned with Business Type defaults but fully customisable per business.

### Communication Style

Formatting and language preferences.

*Example:* Use British English. Always address customers by first name when known. Keep responses under three sentences unless detail is requested.

### Escalation Rules

When AI must stop and hand off to a human.

*Example:* Escalate immediately if the customer mentions a medical emergency, legal threat, or requests a manager.

*Example:* Escalate if the customer asks the same question three times without a satisfactory answer.

### Forbidden Topics

Subjects AI must not discuss or must deflect.

*Example:* Do not provide medical diagnoses. Do not discuss competitor pricing. Do not confirm staff personal contact details.

### Upselling Rules

When and how AI may suggest additional services or deals.

*Example:* When a customer books a haircut, mention the monthly maintenance package if they are a returning client.

*Example:* Never upsell during a complaint conversation.

### Custom Instructions

Free-form owner directives that apply across all AI interactions.

*Example:* "Always mention our new Harrow location when customers ask about parking."

*Example:* "If someone asks about allergies, always recommend they speak to their therapist before treatment."

### Internal Notes

Context for AI and staff that must never be shown to customers.

*Example:* "VIP client — owner handles personally. Do not offer automated booking."

---

# Visibility Levels

Every Brain item has a visibility level that controls who and what can access it.

| Level | Who Sees It | Typical Use |
|-------|-------------|-------------|
| **Customer Visible** | Customers, AI, staff, owner | FAQs, service descriptions, public policies, active deals |
| **AI Only** | AI systems only — not shown in customer-facing UI | Behaviour rules, upselling logic, retrieval hints |
| **Staff Only** | Staff and owner — not shared with customers or AI in customer channels | Internal procedures, staff notes, draft policies |
| **Owner Only** | Owner only | Sensitive commercial terms, confidential strategy |

Visibility ensures the right knowledge reaches the right audience. A refund policy may be customer-visible; the margin on a wedding package may be owner-only.

---

# Validity

Brain items are not always permanent. Validity controls when an item is active.

| Type | Description | Example |
|------|-------------|---------|
| **Permanent** | Active until manually changed or archived | Cancellation policy, core service list |
| **Date Range** | Active between a start and end date | Flash deal, limited promotion |
| **Seasonal** | Recurs on a seasonal cycle | Ramadan offers, Christmas packages, summer campaigns |

When an item expires, AI stops referencing it automatically. Expired items remain in the Brain for history but are not served to customers or AI in live interactions.

---

# Priority

Priority determines retrieval order when multiple Brain items could answer the same question.

| Level | When to Use |
|-------|-------------|
| **High** | Policies, pricing rules, safety information, legal commitments |
| **Medium** | Services, FAQs, standard deals |
| **Low** | Marketing material, general brochures, background context |

High-priority items take precedence. If a brochure mentions a price and the pricing rules say otherwise, the pricing rules win.

---

# Tags

Tags are free-form labels that improve search and grouping across categories and types.

*Examples:* `ramadan`, `bridal`, `laser`, `aftercare`, `vip`, `new-client`, `harrow-location`

A single item can have multiple tags. Tags power filtering in the Brain management UI and improve AI retrieval accuracy.

---

# Search

The Business Brain supports search across all item types and metadata.

**Today (conceptual):**

- Search by title, description, category, and tags
- Filter by type, visibility, validity, priority, and status

**Future:**

- Semantic / vector search across structured knowledge and document contents
- OCR-powered search inside uploaded images and scanned PDFs
- Multilingual search — query in one language, retrieve content in another

Search is available to owners and staff in the Brain management experience. AI uses the same retrieval layer during conversations.

---

# Version History

Every change to a Brain item creates a new version.

Version history records:

- What changed
- Who changed it
- When it changed
- Previous content (for structured knowledge and behaviour settings)

Owners can review history and restore a previous version if a change was made in error.

Version history is essential for audit, compliance, and trust — especially for policies and pricing.

---

# Brain Item Model

Every item in the Business Brain — regardless of type — is described by a common set of attributes. These are product concepts, not database fields.

| Attribute | Description |
|-----------|-------------|
| **Title** | Human-readable name. e.g. "Ramadan Offers 2026", "Refund Policy", "Laser Aftercare" |
| **Category** | Grouping within a type. e.g. Policies → Refunds, Documents → Price Lists |
| **Description** | Summary of what the item contains and when to use it |
| **Priority** | High, Medium, or Low |
| **Visibility** | Customer Visible, AI Only, Staff Only, or Owner Only |
| **Audience** | Who the item is intended for. e.g. New clients, Returning clients, Bridal, VIP |
| **Effective Date** | When the item becomes active (for date-ranged and seasonal items) |
| **Expiry Date** | When the item stops being served (optional) |
| **Status** | Draft, Active, Expired, or Archived |
| **Tags** | Free-form labels for search and filtering |
| **Attachments** | Linked files (PDF, images, etc.) where applicable |
| **Version** | Current version number with full history available |
| **Owner** | The person responsible for keeping the item accurate |
| **Last Updated** | Timestamp of the most recent change |

Not every attribute applies to every type. A greeting behaviour setting has no attachment; a PDF price list has no effective date unless it is time-bound.

---

# Real-World Examples

---

## Example 1: Ramadan Offers

**What the business uploads:**

`Ramadan Offers.pdf` — a brochure listing packages and discounts for the Ramadan period.

**Brain item created:**

| Attribute | Value |
|-----------|-------|
| Title | Ramadan Offers 2026 |
| Type | Deal |
| Category | Holiday Promotions |
| Priority | Medium |
| Visibility | Customer Visible |
| Validity | Date Range (1 Ramadan – 30 Ramadan) |
| Tags | `ramadan`, `packages`, `promotion` |
| Attachment | Ramadan Offers.pdf |

**Customer asks (via WhatsApp):**

> Do you have any Ramadan deals?

**How the AI finds the answer:**

1. AI Receptionist queries the Business Brain for active deals tagged `ramadan`
2. Brain returns the Ramadan Offers item — currently within its effective date range
3. AI reads the structured summary and PDF contents
4. AI responds with available packages, prices, and a link to book — citing the current offer, not an expired one

If the customer asks the same question in July, the item has expired. AI does not mention it.

---

## Example 2: Refund Policy

**Brain item:**

| Attribute | Value |
|-----------|-------|
| Title | Refund Policy |
| Type | Policy → Refund Rules |
| Priority | High |
| Visibility | Customer Visible |
| Validity | Permanent |
| Tags | `refunds`, `policy`, `cancellations` |

**Customer asks:**

> I missed my appointment. Can I get a refund?

**How the AI finds the answer:**

1. AI detects a refund intent
2. Brain retrieves Refund Policy (high priority, customer-visible, active)
3. AI applies the policy — no improvisation
4. AI explains the refund terms clearly and offers to escalate if the customer disputes

---

## Example 3: Laser Aftercare

**Brain item:**

| Attribute | Value |
|-----------|-------|
| Title | Laser Treatment Aftercare |
| Type | Structured Knowledge |
| Category | Aftercare |
| Priority | High |
| Visibility | Customer Visible |
| Audience | Laser clients |
| Tags | `laser`, `aftercare`, `safety` |

**Customer asks (day after treatment):**

> What should I avoid after my laser session yesterday?

**How the AI finds the answer:**

1. AI identifies treatment context (laser) from conversation or booking history
2. Brain retrieves Laser Treatment Aftercare — tagged and categorised for this audience
3. AI delivers aftercare instructions accurately
4. AI escalates if the customer reports an adverse reaction (per escalation rules)

---

## Example 4: Hair Colour Price List

**Brain item:**

| Attribute | Value |
|-----------|-------|
| Title | Hair Colour Price List |
| Type | Document |
| Category | Price Lists |
| Priority | High |
| Visibility | Customer Visible |
| Attachment | Colour_Prices_2026.pdf |
| Tags | `colour`, `pricing`, `hair` |

**Customer asks:**

> How much is balayage for long hair?

**How the AI finds the answer:**

1. AI queries Brain for pricing content tagged `colour` and `hair`
2. Brain returns the price list document and any linked pricing rules
3. Pricing rules take priority over brochure figures if they differ
4. AI quotes the correct price range and offers to book a consultation

---

## Example 5: Wedding Packages

**Brain item:**

| Attribute | Value |
|-----------|-------|
| Title | Wedding Packages 2026 |
| Type | Deal → Packages |
| Priority | Medium |
| Visibility | Customer Visible |
| Validity | Permanent (updated annually) |
| Tags | `wedding`, `bridal`, `packages` |
| Attachment | Wedding_Packages_Brochure.pdf |

**Customer asks:**

> What wedding packages do you offer?

**How the AI finds the answer:**

1. AI retrieves wedding-tagged packages from the Brain
2. AI summarises each package — inclusions, pricing, and booking steps
3. Upselling rules may suggest adding bridesmaid styling if not already mentioned
4. AI offers to connect the customer with the bridal coordinator (escalation or handoff)

---

# Future Modules

The Business Brain is a shared intelligence layer. Future and current Zorovex modules consume it — they do not maintain separate knowledge stores.

| Module | How It Uses the Business Brain |
|--------|-------------------------------|
| **AI Receptionist** | Retrieves FAQs, policies, services, and deals to answer customer messages |
| **Voice Calling Agent** | Uses the same Brain for spoken responses — tone and greeting from behaviour layer |
| **Booking Assistant** | References services, pricing rules, and availability policies during booking flows |
| **Upselling Engine** | Reads active deals, packages, and upselling rules to suggest relevant offers |
| **Campaign Generator** | Draws on deals, marketing material, and business rules to draft campaigns |
| **CRM Recommendations** | Uses customer history + Brain content to suggest next actions for staff |
| **Customer Guidance** | Delivers aftercare, preparation, and follow-up content post-appointment |
| **Escalation Engine** | Applies escalation rules and forbidden topics to decide when humans take over |
| **Analytics** | Reports on which Brain items are retrieved most, gaps in coverage, and expired content |
| **Recommendation Engine** | Matches customer profile and context to relevant services and deals |
| **Future AI Employees** | Each new AI role (e.g. AI Sales Agent, AI Follow-up Agent) reads from the same Brain |

No module should duplicate Brain content locally. One Brain, many consumers.

---

# Future Expansion

The Business Brain is designed to grow without architectural redesign.

**Planned capabilities:**

- **Vector search** — Semantic retrieval across all knowledge types and document contents
- **OCR** — Extract and index text from scanned PDFs and images automatically
- **Embeddings** — Dense representations of Brain items for faster, more accurate AI retrieval
- **Multilingual content** — Store and serve knowledge in multiple languages; AI responds in the customer's language
- **Brain templates by Business Type** — Pre-populated Brain starters for salons, clinics, agencies, and more
- **Brain health score** — Surface gaps: missing policies, expired deals, unanswered FAQ categories
- **Collaborative editing** — Multiple staff members contribute to Brain items with approval workflows
- **External sync** — Import from Google Drive, Notion, or website CMS (future integration)
- **AI-suggested items** — Platform suggests new Brain items based on unanswered customer questions

---

# Related Docs

- [PRODUCT_VISION.md](PRODUCT_VISION.md) — long-term product direction
- [BUSINESS_TYPES.md](BUSINESS_TYPES.md) — industry defaults and Brain templates
- [FEATURE_MATRIX.md](FEATURE_MATRIX.md) — feature availability by plan
- [BUSINESS_BRAIN.md](../05_AI/BUSINESS_BRAIN.md) — AI runtime consumption of the Brain (engineering)
- [KNOWLEDGE.md](../03_Backend/KNOWLEDGE.md) — legacy knowledge module (superseded by Business Brain)
- [PROMPT_STRATEGY.md](../05_AI/PROMPT_STRATEGY.md) — how AI prompts incorporate Brain context
- [ESCALATIONS.md](../05_AI/ESCALATIONS.md) — escalation engine behaviour
