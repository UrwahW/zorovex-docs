# Zorovex Docs

Central documentation for the Zorovex platform — product, architecture, backend, frontend, AI, integrations, deployment, and sprints.

## Structure

```
zorovex-docs/
├── README.md
├── 00_Project/
│   ├── PROJECT_ROADMAP.md
│   ├── RELEASE_PLAN.md
│   ├── CHANGELOG.md
│   ├── DECISIONS.md
│   └── GLOSSARY.md
├── 01_Product/
│   ├── PRODUCT_VISION.md
│   ├── BUSINESS_MODEL.md
│   ├── USER_PERSONAS.md
│   ├── BUSINESS_TYPES.md
│   └── FEATURE_MATRIX.md
├── 02_Architecture/
│   ├── SYSTEM_ARCHITECTURE.md
│   ├── TECH_STACK.md
│   ├── DOMAIN_MODEL.md
│   ├── PERMISSIONS.md
│   ├── EVENT_SYSTEM.md
│   ├── SECURITY.md
│   └── CODING_STANDARDS.md
├── 03_Backend/
│   ├── DATABASE.md
│   ├── API.md
│   ├── AUTHENTICATION.md
│   ├── ORGANIZATIONS.md
│   ├── BUSINESS_SETUP.md
│   ├── CUSTOMERS.md
│   ├── SERVICES.md
│   ├── STAFF.md
│   ├── BOOKINGS.md
│   ├── CONVERSATIONS.md
│   ├── KNOWLEDGE.md
│   ├── JOURNEYS.md
│   ├── AI_RUNTIME.md
│   └── NOTIFICATIONS.md
├── 04_Frontend/
│   ├── UI_SYSTEM.md
│   ├── ROUTING.md
│   ├── STATE_MANAGEMENT.md
│   ├── DASHBOARD.md
│   ├── BUSINESS_SETUP_UI.md
│   ├── CRM_UI.md
│   └── MOBILE_SYNC.md
├── 05_AI/
│   ├── BUSINESS_BRAIN.md
│   ├── CONTEXT_BUILDER.md
│   ├── DECISION_ENGINE.md
│   ├── PROMPT_STRATEGY.md
│   ├── MEMORY.md
│   └── ESCALATIONS.md
├── 06_n8n/
│   ├── OVERVIEW.md
│   ├── WHATSAPP.md
│   ├── FACEBOOK.md
│   ├── INSTAGRAM.md
│   ├── VOICE.md
│   └── AUTOMATIONS.md
├── 07_Deployment/
│   ├── DOCKER.md
│   ├── SERVER.md
│   ├── CI_CD.md
│   ├── BACKUPS.md
│   └── MONITORING.md
└── 08_Sprints/
    ├── Sprint_01.md
    ├── Sprint_02.md
    └── Sprint_03.md
```

## Quick Links

| Section | Purpose |
|---------|---------|
| [00_Project](00_Project/) | Roadmap, releases, changelog, decisions, glossary |
| [01_Product](01_Product/) | Vision, business model, personas, features |
| [02_Architecture](02_Architecture/) | System design, domain model, security |
| [03_Backend](03_Backend/) | API, database, and domain services |
| [04_Frontend](04_Frontend/) | UI system, routing, dashboards |
| [05_AI](05_AI/) | AI runtime, prompts, memory, escalations |
| [06_n8n](06_n8n/) | Channel integrations and automations |
| [07_Deployment](07_Deployment/) | Docker, CI/CD, backups, monitoring |
| [08_Sprints](08_Sprints/) | Sprint planning and retrospectives |

## Conventions

- Each doc starts with a **Status** field (`Draft`, `Review`, `Approved`).
- Cross-link related docs in the **Related Docs** section at the bottom of each file.
- Record architectural decisions in [DECISIONS.md](00_Project/DECISIONS.md).
- Log release changes in [CHANGELOG.md](00_Project/CHANGELOG.md).
