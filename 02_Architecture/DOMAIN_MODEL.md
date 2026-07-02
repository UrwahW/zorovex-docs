# Domain Model

---

# Purpose

Defines the business domains inside Zorovex.

This is not the database schema.

It is the conceptual model.

---

Platform

│

Organizations

│

Workspace

│

Business Profile

├── Catalog
├── Staff
├── Customers
├── Bookings
├── Conversations
├── Knowledge
├── AI Runtime
├── Payments
├── Analytics

---

# Business Catalog

Categories

↓

Services

↓

Packages

↓

Promotions

↓

Pricing Rules

↓

Holiday Rules

↓

Published Catalog

---

# CRM

Customers

↓

Contacts

↓

Communication Threads

↓

Messages

↓

Bookings

↓

Invoices

---

# AI Domain

AI Studio

↓

Receptionist

↓

Goals

↓

Knowledge Sources

↓

AI Runtime

↓

Provider

↓

Inspector

---

# Communication Domain

Channels

↓

Threads

↓

Messages

↓

Attachments

↓

Automation

↓

Notifications

---

# Business Readiness

Identity

Location

Availability

Catalog

Channels

Knowledge

Staff

AI

↓

Readiness Score

---

# Platform Domain

Platform Users

↓

Organizations

↓

Subscriptions

↓

Features

↓

Support Sessions

↓

Customer Success

---

# Relationships

One Organization

owns

many Customers

many Services

many Bookings

many Conversations

many Staff

many Promotions

many Packages

many Pricing Rules

many Channels

many Knowledge Records

One Conversation

contains

many Messages

many Attachments

One Booking

belongs to

one Customer

one Service

one Staff member

One AI Runtime Execution

belongs to

one Conversation

uses

Knowledge

Business Rules

Workflow

Provider

Validation

Confidence

---

# Domain Principles

Every domain owns its own data.

Domains communicate through services and events.

Cross-domain writes are prohibited.

Shared behaviour belongs in application services.

The database follows the domain—not the other way around.