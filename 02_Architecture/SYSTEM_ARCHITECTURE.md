# System Architecture

---

# Philosophy

Zorovex is not an AI chatbot.

It is a Business Operating System.

AI exists to operate on top of deterministic business
systems.

Business systems always come first.

---

# High Level Architecture

                    Platform Console
                           │
              ┌────────────┴─────────────┐
              │                          │
      Organization A             Organization B
              │                          │
       Business Workspace       Business Workspace
              │                          │
      Business Domains          Business Domains
              │
     AI Runtime + Booking + CRM
              │
       Communication Channels

---

# Core Layers

Presentation

↓

Application

↓

Domain

↓

Infrastructure

↓

External Providers

---

# Domain Modules

Organizations

Business Profile

Business Catalog

Customers

Bookings

Communications

Knowledge

AI Runtime

Automation

Payments

Analytics

Notifications

---

# AI Position

Customer

↓

Channel

↓

Conversation

↓

AI Runtime

↓

Business Rules

↓

Knowledge

↓

Workflow

↓

Provider

↓

Customer

---

# Communication Architecture

External Channels

↓

n8n

↓

Rails API

↓

Conversation Engine

↓

AI Runtime

↓

Response

↓

n8n

↓

Provider

---

# Catalog Architecture

Owner

↓

Catalog

↓

Published Commercial Data

↓

Booking Engine

↓

Pricing Engine

↓

AI Runtime

↓

Website Widget

---

# Security Boundary

Platform

↓

Organization

↓

Workspace

↓

User

↓

Role

↓

Permission

↓

Policy

---

# Future Layers

Voice Intelligence

Realtime AI

Customer Memory

Marketplace

Analytics Warehouse

Enterprise Integrations