# ENGINEERING TASK

ID

BOOK-001

Sprint

Sprint 2

Title

Booking Engine

Status

Approved

Depends On

CRM-001

---

# Objective

Implement the complete Booking Engine.

This module provides appointment scheduling, calendar management, availability checking, booking lifecycle management, and CRM integration.

This becomes the single source of truth for every appointment in Zorovex.

AI, Receptionists, WhatsApp, Website Booking and future Voice Agents will all use this module.

---

# Scope

Implement

- Appointment CRUD
- Calendar
- Staff Assignment
- Service Assignment
- Availability Engine
- Booking Status Workflow
- Reschedule
- Cancel
- Notes
- Timeline Integration
- CRM Integration
- Dashboard Statistics

---

# Database

Create

appointments

Columns

id

organization_id

contact_id

service_id

staff_id

starts_at

ends_at

duration_minutes

status

source

notes

cancel_reason

created_by

deleted_at

created_at

updated_at

---

# Status

scheduled

confirmed

checked_in

completed

cancelled

no_show

rescheduled

---

# Booking Source

manual

website

whatsapp

instagram

facebook

phone

walk_in

future_ai

future_voice

---

# Availability Engine

Implement

- Working hours validation
- Staff availability
- Service duration validation
- Conflict detection
- Time slot generation

Double booking is not allowed.

---

# Calendar

Views

- Day
- Week
- Month

Support

- Drag & Drop
- Resize Appointment
- Click to Edit

---

# Backend

Create

Appointment

AppointmentPolicy

AppointmentSerializer

AppointmentValidator

AvailabilityService

BookingService

RescheduleService

CancelService

Commands

Queries

Factories

REST Controllers

---

# API

GET    /api/v1/bookings

GET    /api/v1/bookings/:id

POST   /api/v1/bookings

PATCH  /api/v1/bookings/:id

DELETE /api/v1/bookings/:id

GET    /api/v1/bookings/calendar

GET    /api/v1/bookings/availability

POST   /api/v1/bookings/:id/reschedule

POST   /api/v1/bookings/:id/cancel

---

# CRM Integration

Every booking must

- belong to a Contact
- append timeline activity
- increment bookings_count
- update last_booking_at

---

# Dashboard

Display

Today's Appointments

Upcoming

Completed

Cancelled

Revenue (placeholder)

Most Booked Services

Most Active Staff

---

# Frontend

Create

Booking Dashboard

Calendar

Appointment List

Appointment Details

Create Booking

Edit Booking

Availability Picker

Reschedule Dialog

Cancel Dialog

Booking Filters

---

# Permissions

Owner

Full Access

Manager

Full Access

Receptionist

Create / Update

Marketing

Read Only

Accountant

Read Only

---

# Soft Delete

Use deleted_at.

Never permanently delete appointments.

---

# Logging

AppointmentCreated

AppointmentUpdated

AppointmentCancelled

AppointmentRescheduled

AppointmentCompleted

---

# Events

AppointmentCreated

AppointmentUpdated

AppointmentCancelled

AppointmentCompleted

---

# Out of Scope

Payments

Invoices

SMS

WhatsApp

AI Runtime

Voice Calls

Recurring Appointments

Multi-location Scheduling

---

# Testing

Create

Model Specs

Request Specs

Policy Specs

Service Specs

Availability Specs

Calendar Specs

Frontend Tests

Routing Tests

All tests must pass.

---

# Deliverables

Booking Engine

Calendar

Availability Engine

Appointment CRUD

CRM Integration

Dashboard

REST API

Tests

Engineering Review

---

# Acceptance Criteria

✓ Calendar operational

✓ Availability engine working

✓ Appointment CRUD working

✓ Conflict detection working

✓ CRM timeline updates

✓ Dashboard operational

✓ Tests pass

✓ Rubocop passes

✓ Brakeman passes

Stop after completion.

Generate Engineering Review.

Wait for architect approval.

---

# Completion Report

Populate

98_Engineering_Reviews/Sprint-02/Reviews/BOOK-001.md

Include

- Summary
- Files Created
- Files Modified
- Database Changes
- API Endpoints
- Tests Added
- Assumptions
- Risks
- Technical Debt