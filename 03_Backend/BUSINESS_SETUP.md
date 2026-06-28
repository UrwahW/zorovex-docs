# frozen_string_literal: true

## Overview

Multi-step onboarding wizard. Step 2 (**Location**) collects country, address, timezone, currency, and language on `business_profiles` via `GET/PATCH /api/v1/business/setup/location`.

## Location step (BUS-004)

- **Route (frontend):** `/business/setup/location`
- **API:** `GET/PATCH /api/v1/business/setup/location`
- **Authorization:** Owner/manager write; marketing/accountant read; receptionist 403
- **Auto-save:** 1000ms debounce on the frontend

## Availability step (BUS-005)

- **Route (frontend):** `/business/setup/working-hours`
- **API:** `GET/PATCH /api/v1/business/setup/availability`
- **Data:** `business_availabilities` — seven rows per organization (Mon–Sun)
- **Authorization:** Owner/manager write; marketing/accountant read; receptionist 403
- **Auto-save:** 1000ms debounce; timezone read-only from business profile


- [BUSINESS_PROFILE.md](BUSINESS_PROFILE.md) — profile entity, schema, and API
- [BUSINESS_SETUP_UI.md](../04_Frontend/BUSINESS_SETUP_UI.md) — wizard UI
- [BUSINESS_TYPES.md](../01_Product/BUSINESS_TYPES.md) — supported business types
