# ENGINEERING TASK

ID

CALENDAR-001

Sprint

Sprint 05

Title

Scheduling & Calendar Platform

Status

Approved

Depends On

BOOK-001

OPS-001

PAYMENTS-001

AI-005

PLATFORM-002

---

# Objective

Implement the centralized Scheduling & Calendar Platform.

The Calendar Platform becomes the single source of truth for all scheduled events inside Zorovex.

Every appointment, blocked period, leave request, holiday, AI reservation, reminder and future event must exist inside this platform.

External calendars synchronize with this platform rather than replacing it.

---

# Philosophy

The Business Calendar owns time.

Google Calendar

Outlook

Apple Calendar

are integrations.

Not the source of truth.

---

# Scope

Implement

- Business Calendar
- Staff Calendars
- Resource Calendars
- Calendar Synchronization
- Calendar Availability
- Blocked Time
- Holidays
- Leave Management
- Time Zone Management
- Calendar Events
- External Calendar Providers

---

# Architecture

Booking Engine

↓

Calendar Platform

↓

Availability Engine

↓

External Providers

---

# Calendar Types

Business Calendar

Staff Calendar

Room Calendar (future)

Equipment Calendar (future)

Resource Calendar

Holiday Calendar

AI Calendar

Future Vehicle Calendar

---

# Event Types

Appointment

Blocked Time

Holiday

Leave

Business Closed

Business Open

Meeting

Reminder

Task

Training

Maintenance

Future

Rental

---

# Event Status

Scheduled

Confirmed

Completed

Cancelled

Pending

Tentative

Blocked

---

# Availability Engine

Support

Working Hours

Business Hours

Staff Hours

Breaks

Lunch

Leave

Vacation

Blocked Time

Holiday

Timezone

External Calendar Conflicts

No double bookings.

---

# Recurrence

Support

Daily

Weekly

Monthly

Yearly

Custom

Exclude Dates

Future recurring appointments.

---

# Synchronization

Providers

Google Calendar

Outlook Calendar

Apple Calendar

ICS

---

# Sync Direction

Import

Export

Two-Way

Conflict Resolution

Manual Override

---

# Conflict Detection

Detect

Double Booking

Holiday Conflict

Leave Conflict

Business Closed

Blocked Time

External Calendar Event

Timezone Conflict

---

# AI Integration

AI Runtime

↓

Availability

↓

Booking Workflow

↓

Calendar Reservation

↓

Booking Confirmation

AI may temporarily reserve slots while waiting for payment.

Reservations automatically expire.

---

# Booking Integration

Bookings

↓

Calendar Events

↓

Availability

↓

Notifications

↓

Automations

---

# Operations Integration

Staff schedules

↓

Calendar

↓

Availability

↓

Resource utilization

---

# CRM Integration

Customer timeline

↓

Upcoming appointments

↓

Past appointments

↓

Calendar history

---

# Business Rules

Support

Buffer Time

Cleaning Time

Preparation Time

Travel Time (future)

Maximum Daily Bookings

Maximum Weekly Bookings

Working Days

Blackout Dates

Minimum Notice

Maximum Advance Booking

---

# Calendar Views

Day

Week

Month

Agenda

Timeline

Staff View

Business View

Future Resource View

---

# Search

Search

Customer

Staff

Service

Date

Status

Location

Future Tags

---

# APIs

GET /api/v1/calendar

GET /api/v1/calendar/events

GET /api/v1/calendar/:id

POST /api/v1/calendar/events

PATCH /api/v1/calendar/events/:id

DELETE /api/v1/calendar/events/:id

POST /api/v1/calendar/sync

GET /api/v1/calendar/providers

POST /api/v1/calendar/providers/:id/connect

DELETE /api/v1/calendar/providers/:id/disconnect

---

# Backend

Create

CalendarService

CalendarEventService

AvailabilityService

ConflictDetectionService

CalendarSyncService

ProviderRegistry

GoogleCalendarProvider

OutlookProvider

AppleCalendarProvider

ICSProvider

Policies

Commands

Queries

Validators

Serializers

Factories

Specs

---

# Frontend

Create

Business Calendar

Staff Calendar

Calendar Sidebar

Availability Manager

Holiday Manager

Leave Manager

Sync Settings

Provider Manager

Conflict Viewer

Reservation Viewer

---

# Permissions

Owner

Full

Manager

Manage Calendar

Receptionist

Bookings

Marketing

Read

Accountant

Read

---

# Domain Events

Publish

CalendarEventCreated

CalendarEventUpdated

CalendarEventDeleted

AvailabilityChanged

CalendarSynced

ConflictDetected

LeaveApproved

HolidayCreated

ReservationExpired

---

# Monitoring

Track

Calendar Sync Status

Conflict Count

Availability Changes

Provider Health

Reservation Expiry

Synchronization Failures

---

# Logging

Log

CalendarCreated

CalendarUpdated

CalendarDeleted

ProviderConnected

ProviderDisconnected

SyncStarted

SyncCompleted

ConflictDetected

---

# Testing

Create

Availability Specs

Conflict Specs

Synchronization Specs

Reservation Specs

Provider Specs

API Specs

Frontend Specs

All tests must pass.

---

# Deliverables

Scheduling Platform

Availability Engine

Provider Framework

Business Calendar

Staff Calendar

Conflict Detection

Synchronization

REST APIs

Tests

Engineering Review

---

# Acceptance Criteria

✓ Calendar Platform operational

✓ Availability operational

✓ Conflict Detection operational

✓ Reservations operational

✓ Provider Framework implemented

✓ Synchronization operational

✓ APIs operational

✓ Tests pass

✓ Rubocop passes

✓ Brakeman passes

Stop after completion.

Generate Engineering Review.

Wait for architect approval.

---

# Completion Report

Populate

98_Engineering_Reviews/Sprint-05/Reviews/CALENDAR-001.md

Include

- Summary
- Files Created
- Files Modified
- Database Changes
- Calendar Types
- Event Types
- Availability Rules
- Provider Framework
- API Endpoints
- Domain Events
- Tests Added
- Assumptions
- Risks
- Technical Debt