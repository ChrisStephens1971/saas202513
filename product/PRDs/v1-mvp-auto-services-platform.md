# Auto Services Platform - V1 MVP PRD

**Author:** Product Team
**Date:** 2025-11-09
**Status:** Draft
**Last Updated:** 2025-11-09

---

## 1. Executive Summary

The Auto Services Platform V1 MVP is a complete operational system for mobile detailers (solo to 10-tech operations) that centralizes booking, automates quotes, optimizes routing, and accelerates payments. The MVP delivers on our core promise: **"Never drive dumb, never lose a job to no-shows, and get paid fast"**—setup in under 30 minutes with immediate ROI (+1 job per van per day or ≥15% less drive time).

**Target Launch:** Jun 30, 2025 (full V1) with Validation MVP by Jan 31, 2025

---

## 2. Problem Statement

### What problem are we solving?

Mobile detailers lose 2-4 hours per day to inefficient routing ("windshield time"), 15-20% of jobs to no-shows, and days/weeks waiting for payment. They juggle multiple tools (Google Calendar, pen & paper, Square, scattered texts) with no centralized system for quotes, scheduling, routing, or customer communication.

**Key Pain Points:**
1. **Double-bookings and no-shows** cost $50-150 per missed job
2. **Wasted drive time** prevents +1-2 jobs per van per day (lost $100-300/day revenue)
3. **Ad-hoc quoting** leads to inconsistent pricing and undercharging
4. **Scattered payments** (cash, Venmo, Square) delay cash flow and complicate bookkeeping
5. **Disorganized photos and customer data** make follow-ups and upsells difficult

### Who has this problem?

- **Primary Users:** Solo to 10-tech mobile auto detailers in the US (~28-48K tech-forward operators)
- **Secondary Users (Post-PMF):** Mobile mechanics, mobile car wash operators

**User Persona - "Mike the Mobile Detailer":**
- Age: 28-45
- Business: Solo or 2-5 tech mobile detailing operation
- Revenue: $75-150K/year (solo) or $250-500K/year (team)
- Tech-savvy: Uses Square/Venmo, Google Calendar, Facebook for marketing
- Pain: Spends 10-15 hours/week on admin (scheduling, quoting, chasing payments)
- Goal: Serve 5-8 jobs/day instead of 3-5; reduce no-shows; get paid same-day

### Why is this important now?

- **Market Size:** ~50-80K mobile detailers in US; ~28-48K reachable with tech-forward positioning
- **Revenue Opportunity:** 3% capture at $75 ARPU = $2.0-2.7M ARR; payment fees can double effective ARPU
- **Competitive Gap:** Square/Calendly lack dispatch; Jobber/Housecall Pro are heavy and over-serve small operators
- **Wedge Strategy:** Detailers are simpler than mechanics (no parts inventory); faster path to PMF

---

## 3. Goals and Success Metrics

### Primary Goals

1. **Prove Core Value Prop:** Demonstrate +1 job/van/day OR ≥15% drive time reduction with 20 paid pilots by Feb 28, 2025
2. **Achieve Product-Market Fit:** Reach 100 paying customers by Q2 2025 with <3% monthly churn
3. **Drive Payment Attachment:** ≥70% of jobs processed through platform payments to increase effective ARPU to $120-150/mo

### Key Metrics

| Metric | Baseline (Current State) | V1 Target | Timeline |
|--------|--------------------------|-----------|----------|
| **Booking Conversion** | ~30% (industry avg) | ≥45% | Jun 2025 |
| **No-Show Rate** | ~15-20% (industry avg) | ≤3% (with deposits) | Jun 2025 |
| **Route Utilization** | ~50-60% (service vs. drive time) | ≥80% | Jun 2025 |
| **Self-Scheduled Jobs** | ~10-20% | ≥60% | Jun 2025 |
| **Payment Attach Rate** | 0% (baseline) | ≥70% | Jun 2025 |
| **Setup Time** | N/A | <30 minutes | Jun 2025 |
| **Monthly Churn** | N/A (new product) | <3% | Jun 2025 |
| **Customer Satisfaction (NPS)** | N/A | ≥50 | Jun 2025 |

### Success Criteria for V1 Launch

- [ ] ≥100 paying customers ($49-99/mo)
- [ ] ≥70% payment attach rate (processing ≥70% of jobs through platform)
- [ ] ≥45% booking conversion (customer → completed booking)
- [ ] ≤3% no-show rate (with deposit enforcement)
- [ ] <30 min setup time (onboarding to first booking)
- [ ] <3% monthly churn rate

---

## 4. User Stories

### Epic 1: Smart Booking

**As a** mobile detailer
**I want** customers to self-schedule appointments with real-time availability and automatic deposit collection
**So that** I eliminate double-bookings, reduce no-shows, and spend less time coordinating schedules

**Acceptance Criteria:**
- [ ] Customers can view real-time availability on branded booking page
- [ ] System enforces buffer times between jobs (travel + cleanup)
- [ ] 50% deposit required upfront for all bookings
- [ ] No-show fee ($25-50) automatically charged if customer misses appointment
- [ ] Google Calendar 2-way sync (import existing calendar, export new bookings)
- [ ] SMS confirmation sent immediately upon booking
- [ ] Automated reminder sent 24 hours before appointment

---

### Epic 2: Quote Builder

**As a** mobile detailer
**I want** to create professional quotes with pre-configured packages and add-ons
**So that** I standardize pricing, increase average ticket size, and send quotes in under 2 minutes

**Acceptance Criteria:**
- [ ] Pre-configured service packages (Basic Detail, Full Detail, Premium, etc.)
- [ ] Customizable add-ons (headlight restoration, engine bay, ceramic coating)
- [ ] AI-suggested pricing based on zip code, vehicle type, and market rates
- [ ] Quote sent via SMS/email with online booking link
- [ ] Customer can accept quote and book in one click
- [ ] Track quote-to-booking conversion rate

---

### Epic 3: Dispatch & Routing

**As a** mobile detailer with multiple vans/techs
**I want** optimized routes that minimize drive time and maximize jobs per day
**So that** I can serve +1-2 jobs per van per day and reduce fuel costs by 15-20%

**Acceptance Criteria:**
- [ ] Route optimizer suggests optimal order of jobs to minimize drive time
- [ ] "Swap suggestions" when a better route is possible (e.g., reschedule Job B to tomorrow, add Job C today)
- [ ] Multi-tech assignment (assign jobs to specific technicians)
- [ ] Dynamic ETAs sent to customers as tech approaches
- [ ] Real-time drive time calculation using Google Maps/Mapbox API
- [ ] Route efficiency report (service time vs. drive time)

---

### Epic 4: Payments Integration

**As a** mobile detailer
**I want** to accept payments via card, Apple Pay, and Google Pay with instant payouts
**So that** I improve cash flow, eliminate manual invoicing, and increase payment collection from ~70% to ~95%

**Acceptance Criteria:**
- [ ] Stripe Connect integration for payment processing
- [ ] Card-on-file stored securely with PCI compliance
- [ ] Apple Pay and Google Pay support
- [ ] Automated invoicing after job completion
- [ ] Instant payout option (1% fee) for same-day access to funds
- [ ] Payment reminders for unpaid invoices (auto-sent at 24h, 7d, 14d)
- [ ] Platform fee (1.0-1.5%) added on top of Stripe processing fee

---

### Epic 5: Two-Way Messaging Hub

**As a** mobile detailer
**I want** all customer communication in one place with automated messages and photo sharing
**So that** I reduce back-and-forth, improve customer satisfaction, and build a portfolio of before/after photos

**Acceptance Criteria:**
- [ ] Unified SMS inbox for all customer conversations (via Twilio)
- [ ] Pre-built templates (booking confirmation, day-before reminder, on-the-way, job complete)
- [ ] Photo/video upload from mobile with auto-sharing to customer
- [ ] Automated reminders (24h before, 1h before, on-the-way)
- [ ] Customer can reply to messages (2-way communication)
- [ ] All messages linked to job/customer record

---

### Epic 6: Light CRM

**As a** mobile detailer
**I want** a simple database of customers, vehicles, and service history
**So that** I can track repeat customers, upsell services, and maintain a portfolio of work

**Acceptance Criteria:**
- [ ] Customer profiles with name, phone, email, address
- [ ] Vehicle records (year, make, model, color, VIN)
- [ ] Service history (past jobs, photos, notes)
- [ ] Photo gallery per customer (before/after photos organized by job)
- [ ] Notes/tags on customer records (e.g., "VIP", "Repeat Customer", "Referred by X")
- [ ] Quick lookup by phone number, name, or vehicle

---

## 5. Requirements

### Must Have (P0) - Validation MVP (Jan 31, 2025)

**Core Booking:**
- [ ] Stripe checkout page for subscription signup ($49-99/mo)
- [ ] Basic calendar view with available time slots
- [ ] Deposit collection (50% upfront via Stripe)
- [ ] Google Calendar import (one-way sync)
- [ ] SMS booking confirmation (Twilio)

**Simple Quote Builder:**
- [ ] 3-5 pre-built service packages
- [ ] Custom quote creation form
- [ ] Send quote via SMS with booking link

**Payments:**
- [ ] Stripe payment processing (card, Apple Pay, Google Pay)
- [ ] Manual invoice creation
- [ ] Payment tracking (paid/unpaid)

---

### Must Have (P0) - V1 Full Launch (Jun 30, 2025)

**Smart Booking:**
- [ ] Real-time availability calendar with buffer times
- [ ] Automated deposit collection and no-show fees
- [ ] Google Calendar 2-way sync
- [ ] Automated SMS reminders (24h, 1h, on-the-way)
- [ ] Branded booking pages (white-label for customer acquisition)

**Advanced Quote Builder:**
- [ ] AI-suggested pricing (zip code, vehicle type, market rates)
- [ ] Add-on selection (headlight restoration, ceramic coating, etc.)
- [ ] One-click quote acceptance and booking

**Dispatch & Routing:**
- [ ] Route optimizer (minimize drive time)
- [ ] Multi-tech assignment
- [ ] Dynamic ETA updates sent to customers
- [ ] Route efficiency dashboard

**Payments:**
- [ ] Card-on-file for repeat customers
- [ ] Automated invoicing after job completion
- [ ] Instant payout option (1% fee)
- [ ] Payment reminders (24h, 7d, 14d)

**Messaging Hub:**
- [ ] Unified SMS inbox (Twilio)
- [ ] Pre-built message templates
- [ ] Photo/video upload and sharing
- [ ] 2-way customer communication

**Light CRM:**
- [ ] Customer and vehicle database
- [ ] Service history with photos
- [ ] Quick search by phone, name, vehicle

---

### Should Have (P1) - V1 or Early V2

- [ ] QuickBooks export (revenue, expenses)
- [ ] Yelp/Google Business Messaging integration
- [ ] Referral tracking on branded booking pages
- [ ] Customer loyalty programs (5th wash free)
- [ ] Basic analytics dashboard (revenue, utilization, top customers)

---

### Nice to Have (P2) - V2 Post-PMF

- [ ] Dynamic pricing (distance-based, peak windows)
- [ ] Technician mobile app (time tracking, checklists, photos)
- [ ] Inventory/kit tracking (chemical usage)
- [ ] Customer financing (Affirm/Klarna for large jobs)
- [ ] Multi-location support (franchise management)

---

## 6. User Experience

### User Flow: New Customer Booking (Self-Service)

```
1. Customer lands on branded booking page (e.g., mikesdetailing.autoservices.app)
   ↓
2. Selects service type (Basic Detail, Full Detail, Premium)
   ↓
3. Adds vehicle details (year, make, model)
   ↓
4. Views real-time availability calendar
   ↓
5. Selects preferred time slot
   ↓
6. Enters contact info (name, phone, email, address)
   ↓
7. Pays 50% deposit via Stripe (card, Apple Pay, Google Pay)
   ↓
8. Receives SMS confirmation with job details and tech ETA
   ↓
9. Receives automated reminders (24h before, 1h before, on-the-way)
   ↓
10. Tech completes job, uploads before/after photos
    ↓
11. Customer receives final invoice via SMS/email
    ↓
12. Remaining 50% auto-charged to card on file
    ↓
13. SMS follow-up with photo gallery link and review request
```

---

### User Flow: Operator Creating a Quote

```
1. Operator receives call/text from potential customer
   ↓
2. Opens quote builder in web app
   ↓
3. Selects service package or customizes services
   ↓
4. Adds vehicle details (year, make, model)
   ↓
5. AI suggests price based on zip code and vehicle type
   ↓
6. Operator adjusts price if needed, adds notes
   ↓
7. Sends quote via SMS/email (includes online booking link)
   ↓
8. Customer clicks link, reviews quote, accepts in one click
   ↓
9. Customer is automatically taken to booking flow (Step 4 above)
```

---

### User Flow: Operator Optimizing Daily Routes

```
1. Operator views dashboard with today's jobs
   ↓
2. System suggests optimal route order to minimize drive time
   ↓
3. Operator reviews suggested route on map view
   ↓
4. System shows "swap suggestions" (e.g., "Reschedule Job B to tomorrow, add Job C for better route")
   ↓
5. Operator approves route or makes manual adjustments
   ↓
6. System calculates ETAs for each customer
   ↓
7. Automated SMS sent to customers with tech arrival time
   ↓
8. As tech moves between jobs, dynamic ETA updates sent
   ↓
9. End-of-day report shows: Total drive time, service time, route efficiency (%)
```

---

### Key Interactions

1. **One-Click Quote Acceptance:** Customer receives quote via SMS → clicks link → reviews services → clicks "Accept & Book" → taken directly to booking calendar
2. **Deposit-First Booking:** All bookings require 50% deposit; no deposit = no booking (reduces no-shows from ~15% to ~3%)
3. **Dynamic ETAs:** As tech completes each job, system recalculates ETA for next customer and sends automated update
4. **Photo-First Workflows:** Tech uploads before/after photos immediately after job → photos auto-shared with customer via SMS → customer receives link to full gallery
5. **Swap Suggestions:** When route can be optimized, system proactively suggests: "Reschedule Job X to tomorrow, add Job Y today to save 45 min drive time"

---

### Mockups/Wireframes

*To be created in Figma:*
- [ ] Branded booking page (customer view)
- [ ] Quote builder (operator view)
- [ ] Route optimizer dashboard (operator view)
- [ ] Daily schedule view with job cards
- [ ] SMS messaging inbox
- [ ] Customer profile with service history

---

## 7. Technical Considerations

### Architecture Overview

**Frontend:**
- **Web App (Operator):** React (Next.js) hosted on Azure Container Apps
- **Booking Pages (Customer):** Server-side rendered React with subdomain routing (`{tenant}.autoservices.app`)
- **Admin Dashboard:** React with chart libraries (Recharts, Visx)

**Backend:**
- **API:** Node.js (Express or Fastify) on Azure Container Apps
- **Database:** PostgreSQL 16 on Azure Database for PostgreSQL
- **Caching:** Redis on Azure Cache for Redis

**Third-Party Services:**
- **Payments:** Stripe Connect (sub-accounts per tenant)
- **Messaging:** Twilio (SMS, MMS for photos)
- **Routing:** Mapbox Directions API or Google Maps Directions API
- **Calendar:** Google Calendar API
- **Email:** SendGrid or Azure Communication Services

**Infrastructure:**
- **Hosting:** Azure Container Apps (auto-scaling)
- **Storage:** Azure Blob Storage (before/after photos, media)
- **Secrets:** Azure Key Vault
- **Monitoring:** Azure Application Insights
- **CI/CD:** GitHub Actions

---

### Dependencies

1. **Stripe Connect Approval:** Must be approved for Stripe Connect platform to process payments on behalf of customers
2. **Twilio Phone Number:** Need dedicated phone number for SMS messaging (approx. $1/mo per customer)
3. **Google Calendar API Access:** Require OAuth approval for calendar sync
4. **Mapbox/Google Maps API Key:** For routing optimization and dynamic ETAs
5. **Azure Subscription:** Must provision Container Apps, PostgreSQL, Redis, Blob Storage

---

### API/Integration Requirements

**Stripe Connect:**
- Create Connected Accounts for each operator (tenant)
- Payment Intents for deposits and final charges
- Instant Payouts API (optional, 1% fee)
- Platform fee configuration (1.0-1.5% on top of processing)

**Twilio:**
- Programmable SMS for 2-way messaging
- MMS for photo sharing
- Webhook endpoints for incoming messages
- Phone number provisioning per tenant (optional)

**Google Calendar API:**
- OAuth 2.0 for calendar authorization
- CalDAV or REST API for event sync
- Webhook notifications for external calendar changes

**Mapbox/Google Directions API:**
- Route optimization (multi-stop routing)
- Distance matrix calculations (drive time between jobs)
- Geocoding for address → lat/lng conversion

---

### Data Requirements

**Core Objects:**
- **Tenants:** Operator account details (business name, subdomain, settings)
- **Users:** Operator users and techs (role-based access)
- **Customers:** Customer profiles (name, phone, email, address)
- **Vehicles:** Customer vehicles (year, make, model, VIN, color)
- **Jobs:** Scheduled/completed jobs (date, time, services, status, photos, notes)
- **Quotes:** Pending quotes sent to customers (services, price, status)
- **Technicians:** Tech profiles (name, phone, availability, assigned jobs)
- **Routes:** Daily route plans (ordered jobs, drive times, ETAs)
- **Payments:** Payment records (Stripe payment IDs, amounts, status)
- **Messages:** SMS message history (to/from, timestamp, linked job)
- **Media:** Before/after photos (S3 URLs, linked to jobs)

**Privacy & Compliance:**
- **PCI DSS:** Stripe handles card data; platform never stores raw card numbers
- **GDPR/CCPA:** Provide customer data export and deletion on request
- **SMS Opt-Out:** All SMS messages include opt-out language per TCPA requirements

---

### Multi-Tenant Considerations

**Tenant Isolation:**
- [x] Database queries include `tenant_id` filtering (all queries scoped to tenant)
- [x] Row-Level Security (RLS) policies applied in PostgreSQL
- [x] Blob storage uses tenant-scoped paths (`/tenants/{tenant_id}/media/`)
- [x] Stripe Connected Accounts ensure payment isolation

**Cross-Tenant Access:**
- [x] No cross-tenant access (default for all features)
- [x] Platform admin can view anonymized aggregate metrics (revenue, user counts) but NOT customer PII

**Tenant-Specific Configuration:**
- [x] Subdomain routing (`{tenant}.autoservices.app`)
- [x] Custom branding (logo, colors on booking pages)
- [x] Service catalog (packages, add-ons, pricing) unique per tenant
- [x] Buffer times and no-show fees configurable per tenant
- [x] Stripe platform fee configurable per tenant (1.0-1.5%)

**Performance Impact:**
- Each tenant limited to 10,000 customers (soft limit; expand on request)
- Route optimization limited to 50 jobs/day per tenant (API rate limits)
- Media storage: 10GB per tenant included; $0.10/GB overage

**Data Export/Deletion:**
- [x] Tenant data export via CSV (customers, vehicles, jobs, payments)
- [x] Tenant deletion removes all data (cascade delete with 30-day soft delete)

**See:** `technical/multi-tenant-architecture.md` for implementation patterns

---

## 8. Launch Plan

### Rollout Strategy

**Phase 1: Validation MVP (Jan-Feb 2025)**
- [ ] Internal testing with 2-3 friendly operators
- [ ] Recruit 20 paid pilots ($39-49/mo early-bird pricing)
- [ ] Shadow 5 operators to validate routing algorithm
- [ ] Measure success: +1 job/day OR ≥15% drive time reduction

**Phase 2: V1 Closed Beta (Mar-May 2025)**
- [ ] Complete V1 feature set (routing, messaging, CRM)
- [ ] Invite 50 additional customers (closed beta)
- [ ] Iterate on feedback, optimize UX
- [ ] Refine pricing ($49 Starter, $99 Pro confirmed)

**Phase 3: Public Launch (Jun 2025)**
- [ ] Full V1 release to public
- [ ] Launch SEO utilities (price calculator, scheduler templates, no-show policy generator)
- [ ] Activate supplier partnerships (detailing chemical distributors, tool vans)
- [ ] Referral program on branded booking pages

**Phase 4: Scale (Jul-Dec 2025)**
- [ ] Gradual rollout to all signups (remove waitlist)
- [ ] Launch V2 features (dynamic pricing, tech app)
- [ ] Expand to mobile mechanics (beta)

---

### Success Criteria for Launch

**Validation MVP (Feb 28, 2025):**
- [ ] ≥20 paid pilots
- [ ] ≥70% payment attach rate
- [ ] Demonstrate +1 job/day OR ≥15% drive time reduction
- [ ] Setup time <30 min

**V1 Full Launch (Jun 30, 2025):**
- [ ] ≥100 paying customers
- [ ] <3% monthly churn
- [ ] ≥45% booking conversion
- [ ] ≤3% no-show rate
- [ ] NPS ≥50

---

### Marketing/Communication Plan

**Pre-Launch (Jan-Feb):**
- Facebook groups: Detailing subreddits, Auto Geek, Detailed Image forums
- Creator partnerships: YouTube detailers with rev-share deals
- Supplier partnerships: Chemical distributors (P&S, CarPro) bundle trials with product purchases

**Launch (Jun):**
- Product Hunt launch
- SEO content: "Best Mobile Detailing Software," "How to Reduce No-Shows," "Route Optimization for Detailers"
- Referral program: $50 credit for referrer + 50% off first month for referee

**Post-Launch (Jul-Dec):**
- Case studies: "Mike increased jobs from 4 to 6 per day"
- Supplier co-marketing: Trade show booths (SEMA, Mobile Tech Expo)
- Google/Facebook Ads: Target "mobile detailing software," "detailing business software"

---

## 9. Risks and Mitigations

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| **Pilot Recruitment Failure** (Can't find 20 pilots) | High | Medium | Partner with detailing suppliers for customer lists; offer $39/mo early-bird pricing; leverage Facebook groups |
| **Routing Algorithm Doesn't Deliver Savings** | High | Medium | Shadow 5 operators pre-launch; validate drive time reduction; pivot to deposits/payments as primary value prop if routing underperforms |
| **Stripe Connect Approval Delays** | Medium | Low | Apply for Stripe Connect early (Dec 2024); have backup payment processor (Square, PayPal) |
| **Seasonality & Churn** (Detailers pause in winter) | Medium | High | Offer seasonal pause option ($0/mo, keep data); introduce per-job pricing tier ($5/job, no monthly fee) |
| **Incumbent Lock-In** (Jobber, Housecall Pro) | High | Medium | Build one-click CSV import; offer white-glove migration; use Stripe network tokens to migrate cards |
| **Feature Creep** (Building too much too fast) | Medium | High | Ruthlessly prioritize dispatch, quotes, payments; integrate (don't build) bookkeeping, marketing automation |
| **Twilio SMS Costs** (High volume = high costs) | Medium | Medium | Charge $0.05/SMS after 500 messages/mo; offer email-only option for cost-sensitive customers |
| **Compliance (TCPA, PCI, GDPR)** | High | Low | Use Stripe for PCI compliance; include SMS opt-out in all messages; provide data export/deletion endpoints |

---

## 10. Timeline and Milestones

| Milestone | Target Date | Status | Owner |
|-----------|-------------|--------|-------|
| **Validation MVP Spec Complete** | Nov 15, 2024 | ⏳ In Progress | Product |
| **Dev Environment Setup (Azure)** | Dec 1, 2024 | ⏳ Not Started | Eng |
| **Stripe Connect Integration** | Dec 15, 2024 | ⏳ Not Started | Eng |
| **Basic Booking + Deposits** | Jan 15, 2025 | ⏳ Not Started | Eng |
| **Validation MVP Launch** | Jan 31, 2025 | ⏳ Not Started | Product/Eng |
| **Recruit 20 Paid Pilots** | Feb 28, 2025 | ⏳ Not Started | GTM |
| **V1 Design Complete (Figma)** | Mar 15, 2025 | ⏳ Not Started | Design |
| **Smart Booking System** | Mar 31, 2025 | ⏳ Not Started | Eng |
| **Quote Builder + AI Pricing** | Apr 15, 2025 | ⏳ Not Started | Eng |
| **Dispatch & Routing Engine** | May 15, 2025 | ⏳ Not Started | Eng |
| **Messaging Hub (Twilio)** | May 31, 2025 | ⏳ Not Started | Eng |
| **Light CRM + Photo Galleries** | Jun 15, 2025 | ⏳ Not Started | Eng |
| **Payments (Card-on-File, Invoicing)** | Jun 30, 2025 | ⏳ Not Started | Eng |
| **V1 Full Launch** | Jun 30, 2025 | ⏳ Not Started | Product/Eng/GTM |

---

## 11. Open Questions

- [ ] **Pricing confirmation:** $49 Starter vs. $99 Pro—what features differentiate the plans? (e.g., Starter = 1 tech, 100 jobs/mo; Pro = 5 techs, unlimited jobs, routing)
- [ ] **Platform fee structure:** 1.0% vs. 1.5% on payments—how to position? (e.g., 1.0% for annual plans, 1.5% for monthly)
- [ ] **Twilio phone numbers:** Should each tenant get a dedicated phone number, or use shared pool with sender ID?
- [ ] **AI pricing:** What data sources for market rates? (Yelp reviews, competitor websites, operator surveys)
- [ ] **No-show fee amount:** $25 vs. $50—what's the right balance between deterrence and customer frustration?
- [ ] **Instant payout fee:** 1% platform fee for same-day payout—is this attractive enough? Competitive with Square (1.5%)?
- [ ] **Google Calendar sync:** One-way (import only) or two-way (bidirectional)? Two-way adds complexity but better UX.

---

## 12. Appendix

### Research and References

- **Market Research:** Auto Services SaaS Summary (Nov 2024)
- **Competitor Analysis:** Jobber, Housecall Pro, Square Appointments, Calendly
- **User Interviews:** 10 mobile detailers interviewed (Oct-Nov 2024)
  - Pain points: Drive time (100%), no-shows (90%), payment delays (80%)
  - Willingness to pay: $50-100/mo for +1 job/day

### Related Documents

- **Product Roadmap:** `product/roadmap/2025-product-roadmap.md`
- **Technical Architecture:** `technical/architecture/multi-tenant-saas-architecture.md` (to be created)
- **Go-To-Market Strategy:** `business/gtm-strategy.md` (to be created)
- **Pricing & Economics:** `business/pricing-model.md` (to be created)

---

## Revision History

| Date | Author | Changes |
|------|--------|---------|
| 2025-11-09 | Product Team | Initial V1 MVP PRD created based on Auto Services SaaS Summary |
