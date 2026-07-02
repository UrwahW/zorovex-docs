# ENGINEERING TASK

ID

AUTH-001

Sprint

Sprint 1

Title

Bootstrap Zorovex Backend

---

# Read First

Before writing code, read:

09_Cursor/START_HERE.md

09_Cursor/Cursor_Rules.md

02_Architecture/TECH_STACK.md

02_Architecture/SYSTEM_ARCHITECTURE.md

02_Architecture/CODING_STANDARDS.md

Do not continue unless those documents have been read.

---

# Objective

Create the backend foundation for the Zorovex CRM.

This task is responsible ONLY for bootstrapping the backend.

Authentication is NOT part of this task.

Business logic is NOT part of this task.

No APIs should be created.

No models should be created.

---

# Technical Stack

Ruby on Rails 8

Ruby 3.4+

PostgreSQL

Redis

Docker

RSpec

Rubocop

Brakeman

Rack CORS

Active Storage

Dotenv

---

# Create Rails Project

Inside

backend/

Create a Rails 8 API application.

Use PostgreSQL.

Do not use SQLite.

---

# Configure

Configure:

PostgreSQL

Redis

Rack CORS

Active Storage

Environment Variables

RSpec

Rubocop

Brakeman

Docker

Docker Compose

---

# Folder Structure

Inside app create:

domains/

runtime/

commands/

queries/

services/

jobs/

events/

policies/

serializers/

validators/

---

# Docker

Create containers for:

backend

postgres

redis

mailpit

All containers must communicate through Docker networking.

---

# Environment Variables

Create:

.env.example

Include:

DATABASE_URL

REDIS_URL

SECRET_KEY_BASE

RAILS_MASTER_KEY

MAILPIT_HOST

MAILPIT_PORT

---

# README

Update backend README.

Include:

Requirements

Setup

Docker

Development

Testing

Linting

---

# Out of Scope

Do NOT create:

User model

Organization model

Authentication

JWT

Controllers

Routes

Business logic

---

# Deliverables

Working Rails backend.

Docker.

Redis.

PostgreSQL.

RSpec.

Rubocop.

Brakeman.

Folder structure.

README.

---

# Acceptance Criteria

Backend boots successfully.

Docker Compose works.

Database connects.

Redis connects.

Tests execute.

Rubocop passes.

Brakeman executes.

Stop after completion.