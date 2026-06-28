# Business Types

> Status: Approved

Official list of industries supported by Zorovex. The machine-readable source of truth lives in `backend/config/business_types.yml` and is loaded by `Industries::Catalog`.

## Overview

Zorovex supports **79** business types across 14 categories. Each type defines metadata used by onboarding, module recommendations, and future AI configuration.

## Source of Truth

| Artifact | Location |
|----------|----------|
| Machine-readable catalog | `backend/config/business_types.yml` |
| Application loader | `Industries::Catalog` |
| API | `GET /api/v1/industries` |
| This document | Human-readable reference synced with the catalog |

## Related Docs

- [BUSINESS_PROFILE.md](../03_Backend/BUSINESS_PROFILE.md) — profile entity and `business_type` field
- [BUSINESS_SETUP.md](../03_Backend/BUSINESS_SETUP.md) — onboarding wizard

## Beauty & Wellness

### Salon

| Field | Value |
|-------|-------|
| **Display Name** | Salon |
| **Internal Code** | `salon` |
| **Description** | Full-service hair and beauty salon offering cuts, colour, and styling. |
| **Typical Services** | Haircuts, colouring, styling, treatments |
| **Common Customers** | Individuals seeking personal grooming, relaxation, and aesthetic treatments |
| **Recommended AI Tone** | Warm, welcoming, and style-conscious |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `scissors` |
| **Status** | active |
| **Notes** | Part of the Beauty & Wellness category. |

### Spa

| Field | Value |
|-------|-------|
| **Display Name** | Spa |
| **Internal Code** | `spa` |
| **Description** | Relaxation and wellness spa providing treatments, massages, and body care. |
| **Typical Services** | Massages, facials, body wraps, wellness packages |
| **Common Customers** | Individuals seeking personal grooming, relaxation, and aesthetic treatments |
| **Recommended AI Tone** | Warm, welcoming, and style-conscious |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `sparkles` |
| **Status** | active |
| **Notes** | Part of the Beauty & Wellness category. |

### Barber Shop

| Field | Value |
|-------|-------|
| **Display Name** | Barber Shop |
| **Internal Code** | `barber_shop` |
| **Description** | Men's grooming studio specialising in haircuts, shaves, and beard care. |
| **Typical Services** | Haircuts, shaves, beard trims, grooming |
| **Common Customers** | Individuals seeking personal grooming, relaxation, and aesthetic treatments |
| **Recommended AI Tone** | Warm, welcoming, and style-conscious |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `scissors` |
| **Status** | active |
| **Notes** | Part of the Beauty & Wellness category. |

### Nail Studio

| Field | Value |
|-------|-------|
| **Display Name** | Nail Studio |
| **Internal Code** | `nail_studio` |
| **Description** | Nail art, manicure, pedicure, and gel extension studio. |
| **Typical Services** | Manicures, pedicures, nail art, gel extensions |
| **Common Customers** | Individuals seeking personal grooming, relaxation, and aesthetic treatments |
| **Recommended AI Tone** | Warm, welcoming, and style-conscious |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `hand` |
| **Status** | active |
| **Notes** | Part of the Beauty & Wellness category. |

### Makeup Studio

| Field | Value |
|-------|-------|
| **Display Name** | Makeup Studio |
| **Internal Code** | `makeup_studio` |
| **Description** | Professional makeup services for events, bridal, and editorial work. |
| **Typical Services** | Bridal makeup, event makeup, editorial looks |
| **Common Customers** | Individuals seeking personal grooming, relaxation, and aesthetic treatments |
| **Recommended AI Tone** | Warm, welcoming, and style-conscious |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `palette` |
| **Status** | active |
| **Notes** | Part of the Beauty & Wellness category. |

### Skincare Clinic

| Field | Value |
|-------|-------|
| **Display Name** | Skincare Clinic |
| **Internal Code** | `skincare_clinic` |
| **Description** | Clinical skincare treatments including facials, peels, and dermatology-lite services. |
| **Typical Services** | Facials, chemical peels, skin consultations |
| **Common Customers** | Individuals seeking personal grooming, relaxation, and aesthetic treatments |
| **Recommended AI Tone** | Warm, welcoming, and style-conscious |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `heart-pulse` |
| **Status** | active |
| **Notes** | Part of the Beauty & Wellness category. |

### Hair Clinic

| Field | Value |
|-------|-------|
| **Display Name** | Hair Clinic |
| **Internal Code** | `hair_clinic` |
| **Description** | Specialist hair restoration, transplant consultation, and scalp treatment clinic. |
| **Typical Services** | Scalp treatments, hair restoration consultations |
| **Common Customers** | Individuals seeking personal grooming, relaxation, and aesthetic treatments |
| **Recommended AI Tone** | Warm, welcoming, and style-conscious |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `activity` |
| **Status** | active |
| **Notes** | Part of the Beauty & Wellness category. |

### Laser Clinic

| Field | Value |
|-------|-------|
| **Display Name** | Laser Clinic |
| **Internal Code** | `laser_clinic` |
| **Description** | Laser hair removal, skin rejuvenation, and aesthetic laser treatments. |
| **Typical Services** | Laser hair removal, skin rejuvenation |
| **Common Customers** | Individuals seeking personal grooming, relaxation, and aesthetic treatments |
| **Recommended AI Tone** | Warm, welcoming, and style-conscious |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `zap` |
| **Status** | active |
| **Notes** | Part of the Beauty & Wellness category. |

### Aesthetic Clinic

| Field | Value |
|-------|-------|
| **Display Name** | Aesthetic Clinic |
| **Internal Code** | `aesthetic_clinic` |
| **Description** | Non-surgical aesthetic treatments including injectables and skin tightening. |
| **Typical Services** | Injectables, skin tightening, aesthetic consultations |
| **Common Customers** | Individuals seeking personal grooming, relaxation, and aesthetic treatments |
| **Recommended AI Tone** | Warm, welcoming, and style-conscious |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `syringe` |
| **Status** | active |
| **Notes** | Part of the Beauty & Wellness category. |

## Healthcare

### Medical Clinic

| Field | Value |
|-------|-------|
| **Display Name** | Medical Clinic |
| **Internal Code** | `medical_clinic` |
| **Description** | General or specialist medical practice providing consultations and care. |
| **Typical Services** | Consultations, diagnostics, follow-up care |
| **Common Customers** | Patients and clients seeking medical, dental, or wellness care |
| **Recommended AI Tone** | Professional, calm, and reassuring |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `stethoscope` |
| **Status** | active |
| **Notes** | Part of the Healthcare category. |

### Dental Clinic

| Field | Value |
|-------|-------|
| **Display Name** | Dental Clinic |
| **Internal Code** | `dental_clinic` |
| **Description** | Dental practice offering check-ups, hygiene, and restorative dentistry. |
| **Typical Services** | Check-ups, hygiene, fillings, cosmetic dentistry |
| **Common Customers** | Patients and clients seeking medical, dental, or wellness care |
| **Recommended AI Tone** | Professional, calm, and reassuring |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `smile` |
| **Status** | active |
| **Notes** | Part of the Healthcare category. |

### Physiotherapy

| Field | Value |
|-------|-------|
| **Display Name** | Physiotherapy |
| **Internal Code** | `physiotherapy` |
| **Description** | Physiotherapy and rehabilitation services for injury recovery and mobility. |
| **Typical Services** | Rehab sessions, injury assessment, mobility programmes |
| **Common Customers** | Patients and clients seeking medical, dental, or wellness care |
| **Recommended AI Tone** | Professional, calm, and reassuring |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `accessibility` |
| **Status** | active |
| **Notes** | Part of the Healthcare category. |

### Chiropractic Clinic

| Field | Value |
|-------|-------|
| **Display Name** | Chiropractic Clinic |
| **Internal Code** | `chiropractic_clinic` |
| **Description** | Chiropractic care focused on spinal health and musculoskeletal alignment. |
| **Typical Services** | Adjustments, spinal assessments, pain management |
| **Common Customers** | Patients and clients seeking medical, dental, or wellness care |
| **Recommended AI Tone** | Professional, calm, and reassuring |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `bone` |
| **Status** | active |
| **Notes** | Part of the Healthcare category. |

### Psychology Practice

| Field | Value |
|-------|-------|
| **Display Name** | Psychology Practice |
| **Internal Code** | `psychology_practice` |
| **Description** | Mental health counselling and psychology services for individuals and families. |
| **Typical Services** | Counselling, therapy sessions, assessments |
| **Common Customers** | Patients and clients seeking medical, dental, or wellness care |
| **Recommended AI Tone** | Professional, calm, and reassuring |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `brain` |
| **Status** | active |
| **Notes** | Part of the Healthcare category. |

### Nutrition Clinic

| Field | Value |
|-------|-------|
| **Display Name** | Nutrition Clinic |
| **Internal Code** | `nutrition_clinic` |
| **Description** | Dietary consultation, meal planning, and nutrition coaching clinic. |
| **Typical Services** | Nutrition plans, dietary coaching, weight management |
| **Common Customers** | Patients and clients seeking medical, dental, or wellness care |
| **Recommended AI Tone** | Professional, calm, and reassuring |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `apple` |
| **Status** | active |
| **Notes** | Part of the Healthcare category. |

### Veterinary Clinic

| Field | Value |
|-------|-------|
| **Display Name** | Veterinary Clinic |
| **Internal Code** | `veterinary_clinic` |
| **Description** | Veterinary practice providing medical care for pets and animals. |
| **Typical Services** | Check-ups, vaccinations, surgical care |
| **Common Customers** | Patients and clients seeking medical, dental, or wellness care |
| **Recommended AI Tone** | Professional, calm, and reassuring |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `paw-print` |
| **Status** | active |
| **Notes** | Part of the Healthcare category. |

## Fitness

### Gym

| Field | Value |
|-------|-------|
| **Display Name** | Gym |
| **Internal Code** | `gym` |
| **Description** | Fitness centre with equipment, classes, and membership programmes. |
| **Typical Services** | Memberships, personal training, group classes |
| **Common Customers** | Members and clients pursuing fitness, training, and active lifestyles |
| **Recommended AI Tone** | Energetic, motivating, and supportive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `dumbbell` |
| **Status** | active |
| **Notes** | Part of the Fitness category. |

### Yoga Studio

| Field | Value |
|-------|-------|
| **Display Name** | Yoga Studio |
| **Internal Code** | `yoga_studio` |
| **Description** | Yoga classes and mindfulness sessions for all skill levels. |
| **Typical Services** | Yoga classes, workshops, private sessions |
| **Common Customers** | Members and clients pursuing fitness, training, and active lifestyles |
| **Recommended AI Tone** | Energetic, motivating, and supportive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `flower-2` |
| **Status** | active |
| **Notes** | Part of the Fitness category. |

### Pilates Studio

| Field | Value |
|-------|-------|
| **Display Name** | Pilates Studio |
| **Internal Code** | `pilates_studio` |
| **Description** | Pilates reformer and mat classes focused on core strength and flexibility. |
| **Typical Services** | Reformer classes, mat pilates, private sessions |
| **Common Customers** | Members and clients pursuing fitness, training, and active lifestyles |
| **Recommended AI Tone** | Energetic, motivating, and supportive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `person-standing` |
| **Status** | active |
| **Notes** | Part of the Fitness category. |

### Personal Trainer

| Field | Value |
|-------|-------|
| **Display Name** | Personal Trainer |
| **Internal Code** | `personal_trainer` |
| **Description** | One-to-one or small-group personal training and fitness coaching. |
| **Typical Services** | Personal training, fitness assessments, coaching plans |
| **Common Customers** | Members and clients pursuing fitness, training, and active lifestyles |
| **Recommended AI Tone** | Energetic, motivating, and supportive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `user-check` |
| **Status** | active |
| **Notes** | Part of the Fitness category. |

### Martial Arts Academy

| Field | Value |
|-------|-------|
| **Display Name** | Martial Arts Academy |
| **Internal Code** | `martial_arts_academy` |
| **Description** | Martial arts school offering classes in disciplines such as karate, BJJ, or taekwondo. |
| **Typical Services** | Classes, grading, private coaching |
| **Common Customers** | Members and clients pursuing fitness, training, and active lifestyles |
| **Recommended AI Tone** | Energetic, motivating, and supportive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `swords` |
| **Status** | active |
| **Notes** | Part of the Fitness category. |

### Swimming Academy

| Field | Value |
|-------|-------|
| **Display Name** | Swimming Academy |
| **Internal Code** | `swimming_academy` |
| **Description** | Swimming lessons and aquatic training for children and adults. |
| **Typical Services** | Swimming lessons, lane hire, aquatic coaching |
| **Common Customers** | Members and clients pursuing fitness, training, and active lifestyles |
| **Recommended AI Tone** | Energetic, motivating, and supportive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `waves` |
| **Status** | active |
| **Notes** | Part of the Fitness category. |

## Education

### Academy

| Field | Value |
|-------|-------|
| **Display Name** | Academy |
| **Internal Code** | `academy` |
| **Description** | Training academy delivering structured courses and certifications. |
| **Typical Services** | Courses, certifications, workshops |
| **Common Customers** | Students, parents, and learners enrolling in courses or programmes |
| **Recommended AI Tone** | Encouraging, clear, and informative |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `graduation-cap` |
| **Status** | active |
| **Notes** | Part of the Education category. |

### Tuition Centre

| Field | Value |
|-------|-------|
| **Display Name** | Tuition Centre |
| **Internal Code** | `tuition_centre` |
| **Description** | After-school tuition and exam preparation for students. |
| **Typical Services** | Subject tuition, exam prep, homework support |
| **Common Customers** | Students, parents, and learners enrolling in courses or programmes |
| **Recommended AI Tone** | Encouraging, clear, and informative |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `book-open` |
| **Status** | active |
| **Notes** | Part of the Education category. |

### Coaching Centre

| Field | Value |
|-------|-------|
| **Display Name** | Coaching Centre |
| **Internal Code** | `coaching_centre` |
| **Description** | Competitive exam and career coaching centre. |
| **Typical Services** | Exam coaching, mock tests, career guidance |
| **Common Customers** | Students, parents, and learners enrolling in courses or programmes |
| **Recommended AI Tone** | Encouraging, clear, and informative |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `presentation` |
| **Status** | active |
| **Notes** | Part of the Education category. |

### School

| Field | Value |
|-------|-------|
| **Display Name** | School |
| **Internal Code** | `school` |
| **Description** | Educational institution managing enrolments, classes, and parent communication. |
| **Typical Services** | Classes, enrolments, parent communication |
| **Common Customers** | Students, parents, and learners enrolling in courses or programmes |
| **Recommended AI Tone** | Encouraging, clear, and informative |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `school` |
| **Status** | active |
| **Notes** | Part of the Education category. |

### Language Institute

| Field | Value |
|-------|-------|
| **Display Name** | Language Institute |
| **Internal Code** | `language_institute` |
| **Description** | Language courses and certification preparation institute. |
| **Typical Services** | Language classes, certification prep |
| **Common Customers** | Students, parents, and learners enrolling in courses or programmes |
| **Recommended AI Tone** | Encouraging, clear, and informative |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `languages` |
| **Status** | active |
| **Notes** | Part of the Education category. |

### Music Academy

| Field | Value |
|-------|-------|
| **Display Name** | Music Academy |
| **Internal Code** | `music_academy` |
| **Description** | Music school offering instrument lessons and performance training. |
| **Typical Services** | Instrument lessons, recitals, theory classes |
| **Common Customers** | Students, parents, and learners enrolling in courses or programmes |
| **Recommended AI Tone** | Encouraging, clear, and informative |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `music` |
| **Status** | active |
| **Notes** | Part of the Education category. |

### Art School

| Field | Value |
|-------|-------|
| **Display Name** | Art School |
| **Internal Code** | `art_school` |
| **Description** | Visual arts school with classes in drawing, painting, and design. |
| **Typical Services** | Art classes, workshops, portfolio preparation |
| **Common Customers** | Students, parents, and learners enrolling in courses or programmes |
| **Recommended AI Tone** | Encouraging, clear, and informative |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `palette` |
| **Status** | active |
| **Notes** | Part of the Education category. |

## Professional Services

### Law Firm

| Field | Value |
|-------|-------|
| **Display Name** | Law Firm |
| **Internal Code** | `law_firm` |
| **Description** | Legal practice providing advisory and representation services. |
| **Typical Services** | Legal advice, representation, document drafting |
| **Common Customers** | Business clients and individuals seeking expert advisory services |
| **Recommended AI Tone** | Professional, precise, and trustworthy |
| **Default Modules** | calendar, staff, customers, knowledge, billing |
| **Icon** | `scale` |
| **Status** | active |
| **Notes** | Part of the Professional Services category. |

### Accounting Firm

| Field | Value |
|-------|-------|
| **Display Name** | Accounting Firm |
| **Internal Code** | `accounting_firm` |
| **Description** | Accounting, bookkeeping, and tax advisory firm. |
| **Typical Services** | Bookkeeping, tax returns, advisory |
| **Common Customers** | Business clients and individuals seeking expert advisory services |
| **Recommended AI Tone** | Professional, precise, and trustworthy |
| **Default Modules** | calendar, staff, customers, knowledge, billing |
| **Icon** | `calculator` |
| **Status** | active |
| **Notes** | Part of the Professional Services category. |

### Consultancy

| Field | Value |
|-------|-------|
| **Display Name** | Consultancy |
| **Internal Code** | `consultancy` |
| **Description** | Management and business consultancy serving corporate clients. |
| **Typical Services** | Strategy consulting, audits, advisory retainers |
| **Common Customers** | Business clients and individuals seeking expert advisory services |
| **Recommended AI Tone** | Professional, precise, and trustworthy |
| **Default Modules** | calendar, staff, customers, knowledge, billing |
| **Icon** | `briefcase` |
| **Status** | active |
| **Notes** | Part of the Professional Services category. |

### Marketing Agency

| Field | Value |
|-------|-------|
| **Display Name** | Marketing Agency |
| **Internal Code** | `marketing_agency` |
| **Description** | Digital and traditional marketing agency managing campaigns for clients. |
| **Typical Services** | Campaign management, content, paid media |
| **Common Customers** | Business clients and individuals seeking expert advisory services |
| **Recommended AI Tone** | Professional, precise, and trustworthy |
| **Default Modules** | calendar, staff, customers, knowledge, billing |
| **Icon** | `megaphone` |
| **Status** | active |
| **Notes** | Part of the Professional Services category. |

### Software House

| Field | Value |
|-------|-------|
| **Display Name** | Software House |
| **Internal Code** | `software_house` |
| **Description** | Software development company building custom applications and products. |
| **Typical Services** | Custom development, support, product delivery |
| **Common Customers** | Business clients and individuals seeking expert advisory services |
| **Recommended AI Tone** | Professional, precise, and trustworthy |
| **Default Modules** | calendar, staff, customers, knowledge, billing |
| **Icon** | `code` |
| **Status** | active |
| **Notes** | Part of the Professional Services category. |

### Architecture Firm

| Field | Value |
|-------|-------|
| **Display Name** | Architecture Firm |
| **Internal Code** | `architecture_firm` |
| **Description** | Architecture and design firm managing projects from concept to delivery. |
| **Typical Services** | Design, planning submissions, project management |
| **Common Customers** | Business clients and individuals seeking expert advisory services |
| **Recommended AI Tone** | Professional, precise, and trustworthy |
| **Default Modules** | calendar, staff, customers, knowledge, billing |
| **Icon** | `ruler` |
| **Status** | active |
| **Notes** | Part of the Professional Services category. |

## Automotive

### Workshop

| Field | Value |
|-------|-------|
| **Display Name** | Workshop |
| **Internal Code** | `workshop` |
| **Description** | Auto repair workshop for servicing and mechanical repairs. |
| **Typical Services** | Servicing, diagnostics, repairs |
| **Common Customers** | Vehicle owners needing maintenance, repair, or automotive products |
| **Recommended AI Tone** | Practical, reliable, and straightforward |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `wrench` |
| **Status** | active |
| **Notes** | Part of the Automotive category. |

### Car Detailing

| Field | Value |
|-------|-------|
| **Display Name** | Car Detailing |
| **Internal Code** | `car_detailing` |
| **Description** | Professional car detailing, polishing, and interior restoration. |
| **Typical Services** | Detailing packages, paint correction, interior cleaning |
| **Common Customers** | Vehicle owners needing maintenance, repair, or automotive products |
| **Recommended AI Tone** | Practical, reliable, and straightforward |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `sparkles` |
| **Status** | active |
| **Notes** | Part of the Automotive category. |

### Car Wash

| Field | Value |
|-------|-------|
| **Display Name** | Car Wash |
| **Internal Code** | `car_wash` |
| **Description** | Car wash and express cleaning services. |
| **Typical Services** | Exterior wash, valet, subscription washes |
| **Common Customers** | Vehicle owners needing maintenance, repair, or automotive products |
| **Recommended AI Tone** | Practical, reliable, and straightforward |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `droplets` |
| **Status** | active |
| **Notes** | Part of the Automotive category. |

### Tire Shop

| Field | Value |
|-------|-------|
| **Display Name** | Tire Shop |
| **Internal Code** | `tire_shop` |
| **Description** | Tyre sales, fitting, balancing, and wheel alignment services. |
| **Typical Services** | Tyre sales, fitting, alignment |
| **Common Customers** | Vehicle owners needing maintenance, repair, or automotive products |
| **Recommended AI Tone** | Practical, reliable, and straightforward |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `circle` |
| **Status** | active |
| **Notes** | Part of the Automotive category. |

### Auto Parts

| Field | Value |
|-------|-------|
| **Display Name** | Auto Parts |
| **Internal Code** | `auto_parts` |
| **Description** | Automotive parts retailer or distributor. |
| **Typical Services** | Parts sales, ordering, trade accounts |
| **Common Customers** | Vehicle owners needing maintenance, repair, or automotive products |
| **Recommended AI Tone** | Practical, reliable, and straightforward |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `package` |
| **Status** | active |
| **Notes** | Part of the Automotive category. |

## Hospitality

### Restaurant

| Field | Value |
|-------|-------|
| **Display Name** | Restaurant |
| **Internal Code** | `restaurant` |
| **Description** | Restaurant offering dine-in, takeaway, and reservation services. |
| **Typical Services** | Dine-in, takeaway, reservations, catering |
| **Common Customers** | Diners, guests, and event hosts seeking food, lodging, or venues |
| **Recommended AI Tone** | Friendly, hospitable, and attentive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `utensils` |
| **Status** | active |
| **Notes** | Part of the Hospitality category. |

### Cafe

| Field | Value |
|-------|-------|
| **Display Name** | Cafe |
| **Internal Code** | `cafe` |
| **Description** | Cafe serving beverages, light meals, and casual dining. |
| **Typical Services** | Coffee, light meals, grab-and-go |
| **Common Customers** | Diners, guests, and event hosts seeking food, lodging, or venues |
| **Recommended AI Tone** | Friendly, hospitable, and attentive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `coffee` |
| **Status** | active |
| **Notes** | Part of the Hospitality category. |

### Bakery

| Field | Value |
|-------|-------|
| **Display Name** | Bakery |
| **Internal Code** | `bakery` |
| **Description** | Bakery producing bread, pastries, and custom cakes. |
| **Typical Services** | Bread, pastries, custom cakes |
| **Common Customers** | Diners, guests, and event hosts seeking food, lodging, or venues |
| **Recommended AI Tone** | Friendly, hospitable, and attentive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `cake-slice` |
| **Status** | active |
| **Notes** | Part of the Hospitality category. |

### Hotel

| Field | Value |
|-------|-------|
| **Display Name** | Hotel |
| **Internal Code** | `hotel` |
| **Description** | Hotel or lodging business managing rooms, guests, and amenities. |
| **Typical Services** | Room bookings, guest services, amenities |
| **Common Customers** | Diners, guests, and event hosts seeking food, lodging, or venues |
| **Recommended AI Tone** | Friendly, hospitable, and attentive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `bed` |
| **Status** | active |
| **Notes** | Part of the Hospitality category. |

### Guest House

| Field | Value |
|-------|-------|
| **Display Name** | Guest House |
| **Internal Code** | `guest_house` |
| **Description** | Small guest house or B&B providing short-term accommodation. |
| **Typical Services** | Room bookings, breakfast, local stays |
| **Common Customers** | Diners, guests, and event hosts seeking food, lodging, or venues |
| **Recommended AI Tone** | Friendly, hospitable, and attentive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `home` |
| **Status** | active |
| **Notes** | Part of the Hospitality category. |

### Event Venue

| Field | Value |
|-------|-------|
| **Display Name** | Event Venue |
| **Internal Code** | `event_venue` |
| **Description** | Venue hire for weddings, corporate events, and celebrations. |
| **Typical Services** | Venue hire, event packages, catering coordination |
| **Common Customers** | Diners, guests, and event hosts seeking food, lodging, or venues |
| **Recommended AI Tone** | Friendly, hospitable, and attentive |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `party-popper` |
| **Status** | active |
| **Notes** | Part of the Hospitality category. |

## Retail

### Clothing Store

| Field | Value |
|-------|-------|
| **Display Name** | Clothing Store |
| **Internal Code** | `clothing_store` |
| **Description** | Fashion and apparel retail store. |
| **Typical Services** | Apparel sales, styling advice, alterations coordination |
| **Common Customers** | Shoppers purchasing products in-store or online |
| **Recommended AI Tone** | Helpful, product-focused, and upbeat |
| **Default Modules** | customers, billing, analytics |
| **Icon** | `shirt` |
| **Status** | active |
| **Notes** | Part of the Retail category. |

### Jewelry Store

| Field | Value |
|-------|-------|
| **Display Name** | Jewelry Store |
| **Internal Code** | `jewelry_store` |
| **Description** | Fine jewellery and accessories retailer. |
| **Typical Services** | Jewellery sales, repairs, custom orders |
| **Common Customers** | Shoppers purchasing products in-store or online |
| **Recommended AI Tone** | Helpful, product-focused, and upbeat |
| **Default Modules** | customers, billing, analytics |
| **Icon** | `gem` |
| **Status** | active |
| **Notes** | Part of the Retail category. |

### Electronics Store

| Field | Value |
|-------|-------|
| **Display Name** | Electronics Store |
| **Internal Code** | `electronics_store` |
| **Description** | Consumer electronics and gadget retail store. |
| **Typical Services** | Device sales, repairs, warranties |
| **Common Customers** | Shoppers purchasing products in-store or online |
| **Recommended AI Tone** | Helpful, product-focused, and upbeat |
| **Default Modules** | customers, billing, analytics |
| **Icon** | `smartphone` |
| **Status** | active |
| **Notes** | Part of the Retail category. |

### Furniture Store

| Field | Value |
|-------|-------|
| **Display Name** | Furniture Store |
| **Internal Code** | `furniture_store` |
| **Description** | Furniture and home furnishings showroom. |
| **Typical Services** | Furniture sales, delivery, interior coordination |
| **Common Customers** | Shoppers purchasing products in-store or online |
| **Recommended AI Tone** | Helpful, product-focused, and upbeat |
| **Default Modules** | customers, billing, analytics |
| **Icon** | `sofa` |
| **Status** | active |
| **Notes** | Part of the Retail category. |

### Pharmacy

| Field | Value |
|-------|-------|
| **Display Name** | Pharmacy |
| **Internal Code** | `pharmacy` |
| **Description** | Pharmacy dispensing prescriptions and health products. |
| **Typical Services** | Prescriptions, OTC products, health advice |
| **Common Customers** | Shoppers purchasing products in-store or online |
| **Recommended AI Tone** | Helpful, product-focused, and upbeat |
| **Default Modules** | customers, billing, analytics |
| **Icon** | `pill` |
| **Status** | active |
| **Notes** | Part of the Retail category. |

### Grocery Store

| Field | Value |
|-------|-------|
| **Display Name** | Grocery Store |
| **Internal Code** | `grocery_store` |
| **Description** | Grocery and convenience retail store. |
| **Typical Services** | Groceries, household goods, local delivery |
| **Common Customers** | Shoppers purchasing products in-store or online |
| **Recommended AI Tone** | Helpful, product-focused, and upbeat |
| **Default Modules** | customers, billing, analytics |
| **Icon** | `shopping-cart` |
| **Status** | active |
| **Notes** | Part of the Retail category. |

### Pet Store

| Field | Value |
|-------|-------|
| **Display Name** | Pet Store |
| **Internal Code** | `pet_store` |
| **Description** | Pet supplies, food, and accessories retailer. |
| **Typical Services** | Pet food, accessories, grooming referrals |
| **Common Customers** | Shoppers purchasing products in-store or online |
| **Recommended AI Tone** | Helpful, product-focused, and upbeat |
| **Default Modules** | customers, billing, analytics |
| **Icon** | `dog` |
| **Status** | active |
| **Notes** | Part of the Retail category. |

### Florist

| Field | Value |
|-------|-------|
| **Display Name** | Florist |
| **Internal Code** | `florist` |
| **Description** | Florist creating bouquets, arrangements, and event florals. |
| **Typical Services** | Bouquets, event florals, delivery |
| **Common Customers** | Shoppers purchasing products in-store or online |
| **Recommended AI Tone** | Helpful, product-focused, and upbeat |
| **Default Modules** | customers, billing, analytics |
| **Icon** | `flower` |
| **Status** | active |
| **Notes** | Part of the Retail category. |

## Real Estate

### Real Estate Agency

| Field | Value |
|-------|-------|
| **Display Name** | Real Estate Agency |
| **Internal Code** | `real_estate_agency` |
| **Description** | Property sales and lettings agency. |
| **Typical Services** | Sales, lettings, valuations, viewings |
| **Common Customers** | Buyers, sellers, tenants, and landlords in property transactions |
| **Recommended AI Tone** | Professional, consultative, and knowledgeable |
| **Default Modules** | calendar, staff, customers, analytics |
| **Icon** | `building-2` |
| **Status** | active |
| **Notes** | Part of the Real Estate category. |

### Property Management

| Field | Value |
|-------|-------|
| **Display Name** | Property Management |
| **Internal Code** | `property_management` |
| **Description** | Property management company overseeing rentals and maintenance. |
| **Typical Services** | Tenant management, maintenance, rent collection |
| **Common Customers** | Buyers, sellers, tenants, and landlords in property transactions |
| **Recommended AI Tone** | Professional, consultative, and knowledgeable |
| **Default Modules** | calendar, staff, customers, analytics |
| **Icon** | `key` |
| **Status** | active |
| **Notes** | Part of the Real Estate category. |

### Construction Company

| Field | Value |
|-------|-------|
| **Display Name** | Construction Company |
| **Internal Code** | `construction_company` |
| **Description** | Construction firm managing builds, contractors, and projects. |
| **Typical Services** | Build projects, renovations, contractor coordination |
| **Common Customers** | Buyers, sellers, tenants, and landlords in property transactions |
| **Recommended AI Tone** | Professional, consultative, and knowledgeable |
| **Default Modules** | calendar, staff, customers, analytics |
| **Icon** | `hard-hat` |
| **Status** | active |
| **Notes** | Part of the Real Estate category. |

## Home Services

### Cleaning Service

| Field | Value |
|-------|-------|
| **Display Name** | Cleaning Service |
| **Internal Code** | `cleaning_service` |
| **Description** | Residential and commercial cleaning services. |
| **Typical Services** | Regular cleaning, deep cleans, move-out cleans |
| **Common Customers** | Homeowners and businesses needing maintenance and improvement services |
| **Recommended AI Tone** | Reliable, practical, and service-oriented |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `spray-can` |
| **Status** | active |
| **Notes** | Part of the Home Services category. |

### Plumbing

| Field | Value |
|-------|-------|
| **Display Name** | Plumbing |
| **Internal Code** | `plumbing` |
| **Description** | Plumbing installation, repair, and emergency call-out services. |
| **Typical Services** | Repairs, installations, emergency call-outs |
| **Common Customers** | Homeowners and businesses needing maintenance and improvement services |
| **Recommended AI Tone** | Reliable, practical, and service-oriented |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `pipette` |
| **Status** | active |
| **Notes** | Part of the Home Services category. |

### Electrical Services

| Field | Value |
|-------|-------|
| **Display Name** | Electrical Services |
| **Internal Code** | `electrical_services` |
| **Description** | Licensed electrical installation and repair services. |
| **Typical Services** | Installations, fault finding, safety checks |
| **Common Customers** | Homeowners and businesses needing maintenance and improvement services |
| **Recommended AI Tone** | Reliable, practical, and service-oriented |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `zap` |
| **Status** | active |
| **Notes** | Part of the Home Services category. |

### HVAC

| Field | Value |
|-------|-------|
| **Display Name** | HVAC |
| **Internal Code** | `hvac` |
| **Description** | Heating, ventilation, and air conditioning installation and maintenance. |
| **Typical Services** | Installation, servicing, emergency repairs |
| **Common Customers** | Homeowners and businesses needing maintenance and improvement services |
| **Recommended AI Tone** | Reliable, practical, and service-oriented |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `thermometer` |
| **Status** | active |
| **Notes** | Part of the Home Services category. |

### Pest Control

| Field | Value |
|-------|-------|
| **Display Name** | Pest Control |
| **Internal Code** | `pest_control` |
| **Description** | Pest inspection, treatment, and prevention services. |
| **Typical Services** | Inspections, treatments, prevention plans |
| **Common Customers** | Homeowners and businesses needing maintenance and improvement services |
| **Recommended AI Tone** | Reliable, practical, and service-oriented |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `bug` |
| **Status** | active |
| **Notes** | Part of the Home Services category. |

### Interior Design

| Field | Value |
|-------|-------|
| **Display Name** | Interior Design |
| **Internal Code** | `interior_design` |
| **Description** | Interior design studio offering consultation and project management. |
| **Typical Services** | Design consultation, sourcing, project management |
| **Common Customers** | Homeowners and businesses needing maintenance and improvement services |
| **Recommended AI Tone** | Reliable, practical, and service-oriented |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `paintbrush` |
| **Status** | active |
| **Notes** | Part of the Home Services category. |

## Photography & Media

### Photography Studio

| Field | Value |
|-------|-------|
| **Display Name** | Photography Studio |
| **Internal Code** | `photography_studio` |
| **Description** | Photography studio for portraits, events, and commercial shoots. |
| **Typical Services** | Portraits, events, commercial photography |
| **Common Customers** | Clients booking creative production and media services |
| **Recommended AI Tone** | Creative, polished, and personable |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `camera` |
| **Status** | active |
| **Notes** | Part of the Photography & Media category. |

### Videography Studio

| Field | Value |
|-------|-------|
| **Display Name** | Videography Studio |
| **Internal Code** | `videography_studio` |
| **Description** | Video production studio for events, corporate, and creative content. |
| **Typical Services** | Event video, corporate films, editing |
| **Common Customers** | Clients booking creative production and media services |
| **Recommended AI Tone** | Creative, polished, and personable |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `video` |
| **Status** | active |
| **Notes** | Part of the Photography & Media category. |

### Printing Press

| Field | Value |
|-------|-------|
| **Display Name** | Printing Press |
| **Internal Code** | `printing_press` |
| **Description** | Commercial printing for marketing materials, signage, and packaging. |
| **Typical Services** | Print runs, signage, packaging |
| **Common Customers** | Clients booking creative production and media services |
| **Recommended AI Tone** | Creative, polished, and personable |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `printer` |
| **Status** | active |
| **Notes** | Part of the Photography & Media category. |

### Advertising Agency

| Field | Value |
|-------|-------|
| **Display Name** | Advertising Agency |
| **Internal Code** | `advertising_agency` |
| **Description** | Creative advertising agency for brand and campaign production. |
| **Typical Services** | Creative campaigns, media buying, branding |
| **Common Customers** | Clients booking creative production and media services |
| **Recommended AI Tone** | Creative, polished, and personable |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `monitor` |
| **Status** | active |
| **Notes** | Part of the Photography & Media category. |

## Travel

### Travel Agency

| Field | Value |
|-------|-------|
| **Display Name** | Travel Agency |
| **Internal Code** | `travel_agency` |
| **Description** | Travel agency booking flights, hotels, and holiday packages. |
| **Typical Services** | Flights, hotels, holiday packages |
| **Common Customers** | Travellers planning trips, tours, and visa applications |
| **Recommended AI Tone** | Adventurous, helpful, and detail-oriented |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `plane` |
| **Status** | active |
| **Notes** | Part of the Travel category. |

### Visa Consultancy

| Field | Value |
|-------|-------|
| **Display Name** | Visa Consultancy |
| **Internal Code** | `visa_consultancy` |
| **Description** | Visa application advisory and documentation consultancy. |
| **Typical Services** | Visa advisory, documentation, application support |
| **Common Customers** | Travellers planning trips, tours, and visa applications |
| **Recommended AI Tone** | Adventurous, helpful, and detail-oriented |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `file-text` |
| **Status** | active |
| **Notes** | Part of the Travel category. |

### Tour Operator

| Field | Value |
|-------|-------|
| **Display Name** | Tour Operator |
| **Internal Code** | `tour_operator` |
| **Description** | Tour operator organising guided tours and travel experiences. |
| **Typical Services** | Guided tours, packages, group travel |
| **Common Customers** | Travellers planning trips, tours, and visa applications |
| **Recommended AI Tone** | Adventurous, helpful, and detail-oriented |
| **Default Modules** | bookings, calendar, staff, customers, knowledge |
| **Icon** | `map` |
| **Status** | active |
| **Notes** | Part of the Travel category. |

## Religious & Community

### Mosque

| Field | Value |
|-------|-------|
| **Display Name** | Mosque |
| **Internal Code** | `mosque` |
| **Description** | Mosque managing community programmes, events, and congregation services. |
| **Typical Services** | Prayer services, community events, education programmes |
| **Common Customers** | Congregation members, donors, volunteers, and community participants |
| **Recommended AI Tone** | Respectful, warm, and community-focused |
| **Default Modules** | calendar, customers, knowledge |
| **Icon** | `moon` |
| **Status** | active |
| **Notes** | Part of the Religious & Community category. |

### Church

| Field | Value |
|-------|-------|
| **Display Name** | Church |
| **Internal Code** | `church` |
| **Description** | Church coordinating services, community outreach, and member engagement. |
| **Typical Services** | Services, outreach, member groups |
| **Common Customers** | Congregation members, donors, volunteers, and community participants |
| **Recommended AI Tone** | Respectful, warm, and community-focused |
| **Default Modules** | calendar, customers, knowledge |
| **Icon** | `church` |
| **Status** | active |
| **Notes** | Part of the Religious & Community category. |

### NGO

| Field | Value |
|-------|-------|
| **Display Name** | NGO |
| **Internal Code** | `ngo` |
| **Description** | Non-governmental organisation managing programmes, donors, and volunteers. |
| **Typical Services** | Programmes, donor management, volunteer coordination |
| **Common Customers** | Congregation members, donors, volunteers, and community participants |
| **Recommended AI Tone** | Respectful, warm, and community-focused |
| **Default Modules** | calendar, customers, knowledge |
| **Icon** | `heart-handshake` |
| **Status** | active |
| **Notes** | Part of the Religious & Community category. |

### Charity

| Field | Value |
|-------|-------|
| **Display Name** | Charity |
| **Internal Code** | `charity` |
| **Description** | Registered charity coordinating fundraising, aid, and community support. |
| **Typical Services** | Fundraising, aid distribution, community support |
| **Common Customers** | Congregation members, donors, volunteers, and community participants |
| **Recommended AI Tone** | Respectful, warm, and community-focused |
| **Default Modules** | calendar, customers, knowledge |
| **Icon** | `hand-heart` |
| **Status** | active |
| **Notes** | Part of the Religious & Community category. |

### Community Centre

| Field | Value |
|-------|-------|
| **Display Name** | Community Centre |
| **Internal Code** | `community_centre` |
| **Description** | Community centre hosting events, classes, and local services. |
| **Typical Services** | Classes, events, local services |
| **Common Customers** | Congregation members, donors, volunteers, and community participants |
| **Recommended AI Tone** | Respectful, warm, and community-focused |
| **Default Modules** | calendar, customers, knowledge |
| **Icon** | `users` |
| **Status** | active |
| **Notes** | Part of the Religious & Community category. |

## Other

### Coworking Space

| Field | Value |
|-------|-------|
| **Display Name** | Coworking Space |
| **Internal Code** | `coworking_space` |
| **Description** | Coworking space managing desks, memberships, and meeting rooms. |
| **Typical Services** | Desk memberships, meeting rooms, hot desks |
| **Common Customers** | Varied customer base depending on business model |
| **Recommended AI Tone** | Adaptable, friendly, and professional |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `building` |
| **Status** | active |
| **Notes** | Part of the Other category. |

### Event Planner

| Field | Value |
|-------|-------|
| **Display Name** | Event Planner |
| **Internal Code** | `event_planner` |
| **Description** | Event planning and coordination for corporate and private clients. |
| **Typical Services** | Event planning, vendor coordination, timelines |
| **Common Customers** | Varied customer base depending on business model |
| **Recommended AI Tone** | Adaptable, friendly, and professional |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `calendar-heart` |
| **Status** | active |
| **Notes** | Part of the Other category. |

### Rental Business

| Field | Value |
|-------|-------|
| **Display Name** | Rental Business |
| **Internal Code** | `rental_business` |
| **Description** | Equipment or property rental business with booking and inventory management. |
| **Typical Services** | Rentals, bookings, inventory tracking |
| **Common Customers** | Varied customer base depending on business model |
| **Recommended AI Tone** | Adaptable, friendly, and professional |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `key-round` |
| **Status** | active |
| **Notes** | Part of the Other category. |

### Custom Business

| Field | Value |
|-------|-------|
| **Display Name** | Custom Business |
| **Internal Code** | `custom_business` |
| **Description** | Flexible business type for organisations that do not fit a predefined category. |
| **Typical Services** | Configurable services based on business needs |
| **Common Customers** | Varied customer base depending on business model |
| **Recommended AI Tone** | Adaptable, friendly, and professional |
| **Default Modules** | bookings, calendar, staff, customers |
| **Icon** | `settings` |
| **Status** | active |
| **Notes** | Part of the Other category. |

