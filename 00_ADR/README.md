# Architecture Decision Records (ADR)

## Purpose

Architecture Decision Records (ADRs) capture the important technical decisions made during the development of Zorovex.

An ADR explains:

- What decision was made
- Why it was made
- Alternatives considered
- Trade-offs
- Consequences

ADRs exist so that future developers understand not only *what* the system does, but *why* it was designed that way.

---

## Rules

Every architectural decision receives a unique ADR.

Once accepted:

- Engineering tasks must follow the ADR.
- Cursor must not override ADR decisions.
- Any future change requires a new ADR.

Never edit an old ADR to change history.

Instead:

Create a new ADR that supersedes the previous one.

---

## ADR Format

Each ADR contains:

- Status
- Context
- Decision
- Alternatives
- Consequences
- Future Considerations

---

## Status Values

Proposed

Accepted

Deprecated

Superseded

---

## Naming

ADR-001-Technology-Stack.md

ADR-002-Authentication.md

ADR-003-RBAC.md

etc.

---

## Authority

Architecture decisions are made by the project architect.

Cursor may recommend changes but may never change an accepted ADR automatically.

---

## Pending Decisions

Decisions identified during engineering reviews that require a formal ADR are tracked in [PENDING_ADRS.md](PENDING_ADRS.md).