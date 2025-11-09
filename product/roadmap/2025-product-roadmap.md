# Product Roadmap - Auto Services SaaS 2025

**Period:** 2025 Full Year
**Owner:** Product Team
**Last Updated:** 2025-11-09
**Status:** Draft

---

## Vision & Strategy

### Product Vision

Build the essential operating system for mobile auto service businesses (detailers and mechanics) that eliminates wasted drive time, prevents no-shows, and accelerates cash flow. We enable solo operators and small teams to serve +1 job per van per day through intelligent routing, deposit-first booking, and seamless payments—all in under 30 minutes of setup.

**Target:** Become the default platform for 3% of tech-forward mobile detailers (~840-1,440 businesses) within 18 months, generating $2.0-2.7M ARR with payment attach doubling effective ARPU.

### Strategic Themes for 2025

1. **Validation & PMF (Q1-Q2):** Prove core value prop with 20 paid pilots; measure +1 job/day or ≥15% drive time reduction
2. **Scale the Core (Q3):** Launch V1 to broader market; achieve <2% monthly churn through calendar lock-in and payment attachment
3. **Expand Revenue (Q4):** Increase ARPU through payments (≥70% attach) and Teams pricing ($149 + $10/tech)

---

## Roadmap Overview

### Now (Jan-Feb 2025) - Validation MVP
**Focus:** Sell first, validate core hypotheses with 20 paid pilots

| Feature/Initiative | Status | Owner | Target Date | Priority |
|--------------------|--------|-------|-------------|----------|
| Stripe checkout + basic scheduler | Not Started | Eng | Jan 31 | P0 |
| Deposit flows (50% upfront) | Not Started | Eng | Jan 31 | P0 |
| Google Calendar import | Not Started | Eng | Feb 7 | P0 |
| SMS reminders (Twilio) | Not Started | Eng | Feb 14 | P1 |
| Simple quote builder (packages) | Not Started | Eng | Feb 21 | P0 |
| Pilot recruitment (20 detailers) | Not Started | GTM | Feb 28 | P0 |

**Success Criteria:**
- ≥20 paid pilots ($49-99/mo)
- ≥15% reduction in drive time OR +1 job/van/day
- ≥70% payment attach rate
- No-shows ≤3% with deposits

---

### Next (Mar-Jun 2025) - V1 Full Launch
**Focus:** Complete "Win the Day" feature set; launch to broader market

| Feature/Initiative | Description | Strategic Theme | Target Date | Priority |
|--------------------|-------------|-----------------|-------------|----------|
| Smart Booking System | Real-time availability, buffers, no-show fees, customer self-scheduling | Validation & PMF | Mar 31 | P0 |
| Advanced Quote Builder | Add-ons, AI price suggestions (based on zip, vehicle type), service packages | Validation & PMF | Apr 15 | P0 |
| Dispatch & Routing Engine | Route optimizer, multi-tech assignment, dynamic ETAs, "swap suggestions" | Validation & PMF | May 15 | P0 |
| Two-Way Messaging Hub | SMS templates, photo/video intake, automated reminders, job updates | Validation & PMF | May 31 | P0 |
| Light CRM | Customers, vehicles, service history, photo galleries, notes | Validation & PMF | Jun 15 | P1 |
| Payments Integration | Card-on-file, Apple/Google Pay, instant payout option (Stripe), invoicing | Expand Revenue | Jun 30 | P0 |
| Branded Booking Pages | White-label scheduling pages for customer acquisition, referral tracking | Scale the Core | Jun 30 | P1 |

**Success Criteria:**
- Booking conversion ≥45%
- Route utilization ≥80% service time
- Self-scheduled jobs ≥60%
- Payment attach ≥70%
- Setup time <30 minutes

---

### Later (Jul-Dec 2025) - V2 Post-PMF
**Focus:** Reduce churn, increase ARPU, prepare for mobile mechanics expansion

| Feature/Initiative | Description | Strategic Theme | Estimated Quarter | Priority |
|--------------------|-------------|-----------------|-------------------|----------|
| Dynamic Pricing Engine | Distance-based pricing, peak window multipliers, demand pricing | Expand Revenue | Q3 2025 | P1 |
| Technician Mobile App | Time tracking, checklists, before/after photos, parts tracking, offline-tolerant | Scale the Core | Q3 2025 | P0 |
| Inventory & Kit Tracking | Chemical/supply tracking for detailers, parts inventory for mechanics | Scale the Core | Q4 2025 | P2 |
| QuickBooks Integration | Auto-sync revenue, expenses, payroll; export for bookkeeping | Scale the Core | Q4 2025 | P1 |
| Customer Financing | Buy-now-pay-later for large repairs (Affirm/Klarna), optional protection plans | Expand Revenue | Q4 2025 | P2 |
| Teams & Multi-Tech Management | Role permissions, tech performance dashboards, capacity planning | Expand Revenue | Q4 2025 | P1 |
| Analytics Dashboard | Job profitability, route efficiency, tech utilization, customer LTV | Scale the Core | Q4 2025 | P1 |

**Success Criteria:**
- Monthly churn <2%
- Net Revenue Retention >110%
- ARPU increases to $120-150 (with payments)
- ≥50% of customers on Teams plan (multi-tech)

---

### Future/Backlog (2026+)

**Mobile Mechanics Expansion:**
- Diagnostic tools integration (OBD-II readers)
- Parts sourcing marketplace
- Warranty tracking
- Fleet/dealer partnerships for multi-van wins

**Advanced Features:**
- Customer loyalty programs
- Review automation (Yelp/Google)
- Marketing automation (email campaigns, win-back flows)
- Advanced reporting (P&L by service line, customer cohorts)
- API for third-party integrations

**Scale Infrastructure:**
- Multi-location support
- Franchise management tools
- White-label platform for larger operators

---

## Detailed Feature Breakdown

### Smart Booking System

**Problem:** Double-bookings, no-shows, and ad-hoc scheduling waste time and revenue
**Solution:** Real-time calendar with buffer times, deposit requirements (50% upfront), automated no-show fees, self-service customer scheduling
**Impact:**
- Reduce no-shows from ~15-20% to ≤3%
- Enable ≥60% self-scheduled jobs
- Improve booking conversion to ≥45%

**Effort:** Large (4-6 weeks)
**Dependencies:** Google Calendar API, payment processing
**Status:** Not Started
**Target:** Mar 31, 2025
**PRD:** `product/PRDs/smart-booking-system.md`

---

### Dispatch & Routing Engine

**Problem:** Inefficient routing wastes 2-4 hours/day per van ("windshield time")
**Solution:** AI-powered route optimizer with "swap suggestions" to minimize drive time, multi-tech assignment, dynamic ETAs sent to customers
**Impact:**
- Reduce drive time by ≥15%
- Enable +1 job per van per day
- Achieve ≥80% route utilization (service time vs. drive time)

**Effort:** Large (6-8 weeks)
**Dependencies:** Mapbox/Google Directions API, job scheduling system
**Status:** Not Started
**Target:** May 15, 2025
**PRD:** `product/PRDs/dispatch-routing-engine.md`

---

### Quote Builder with AI Pricing

**Problem:** Ad-hoc quotes lead to inconsistent pricing and lost revenue
**Solution:** Service packages, customizable add-ons, AI-suggested pricing based on zip code, vehicle type, and market rates
**Impact:**
- Increase quote-to-booking conversion
- Standardize pricing across technicians
- Optimize revenue per job (+10-15%)

**Effort:** Medium (3-4 weeks)
**Dependencies:** Service catalog, vehicle database
**Status:** Not Started
**Target:** Apr 15, 2025
**PRD:** `product/PRDs/quote-builder.md`

---

### Payments Integration (Stripe)

**Problem:** Scattered payment methods, slow cash flow, manual invoicing
**Solution:** Card-on-file, Apple/Google Pay, automated invoicing, instant payout option (1% fee), payment attach on every job
**Impact:**
- ≥70% payment attach rate
- Double effective ARPU (1.0-1.5% platform fee on payment volume)
- Improve cash flow (instant vs. 30-day payment terms)

**Effort:** Medium (3-4 weeks)
**Dependencies:** Stripe Connect, PCI compliance
**Status:** Not Started
**Target:** Jun 30, 2025
**PRD:** `product/PRDs/payments-integration.md`

---

### Technician Mobile App

**Problem:** Technicians lack tools for time tracking, photo documentation, checklists in the field
**Solution:** Offline-tolerant React Native app with job details, before/after photos, service checklists, parts/supplies tracking
**Impact:**
- Improve service quality (photo documentation)
- Reduce errors (checklists)
- Enable offline work (sync when online)

**Effort:** Large (8-10 weeks)
**Dependencies:** Job management system, media storage
**Status:** Not Started
**Target:** Q3 2025
**PRD:** `product/PRDs/technician-mobile-app.md`

---

### Two-Way Messaging Hub

**Problem:** Customers and techs use scattered communication (text, WhatsApp, email)
**Solution:** Unified SMS hub with templates, photo/video sharing, automated reminders (day-before, on-the-way), job updates
**Impact:**
- Reduce missed appointments
- Improve customer satisfaction
- Centralize communication history

**Effort:** Medium (4 weeks)
**Dependencies:** Twilio integration
**Status:** Not Started
**Target:** May 31, 2025
**PRD:** `product/PRDs/messaging-hub.md`

---

## Success Metrics

### Key Results for 2025

| Metric | Q1 Target | Q2 Target | Q3 Target | Q4 Target |
|--------|-----------|-----------|-----------|-----------|
| Paid Customers | 20 pilots | 100 | 400 | 840-1,440 |
| Monthly Recurring Revenue (MRR) | $1.5K | $7.5K | $30K | $63-108K |
| Annual Recurring Revenue (ARR) | — | — | — | $756K-1.3M |
| Monthly Churn Rate | 5-6% | 3-4% | 2-3% | <2% |
| Payment Attach Rate | 70% | 70% | 75% | 80% |
| Booking Conversion | — | 45% | 50% | 55% |
| No-Show Rate (with deposits) | — | 3% | 2% | 2% |
| Route Utilization | — | 75% | 80% | 85% |
| Self-Scheduled Jobs | — | 60% | 65% | 70% |
| Net Revenue Retention (NRR) | — | — | 105% | >110% |
| Customer Acquisition Cost (CAC) | $150 | $120 | $100 | $80-100 |
| Customer Lifetime Value (LTV) | $2,500 | $3,500 | $4,500 | $4,950+ |

---

## Resource Allocation

### Team Capacity
- **Engineering:** 2-3 full-stack developers (React, React Native, Node.js, Postgres)
- **Design:** 1 product designer (contractor or part-time)
- **Product:** Solo founder / 1 PM

### Effort Distribution (Q1-Q2)
- 70% - V1 MVP features (booking, routing, payments, messaging)
- 15% - Pilot feedback & iteration
- 10% - Infrastructure & DevOps (Azure deployment, monitoring)
- 5% - Technical debt / Performance

### Effort Distribution (Q3-Q4)
- 50% - V2 features (dynamic pricing, tech app, integrations)
- 25% - Scale & performance (handle 400+ customers)
- 15% - Bug fixes & maintenance
- 10% - Experimentation (new verticals, pricing tests)

---

## Risks and Dependencies

| Risk/Dependency | Impact | Mitigation | Owner |
|-----------------|--------|------------|-------|
| **Seasonality & Price Sensitivity** | High - Mobile detailing slows in winter; operators may churn | Offer seasonal pause option, introduce per-job pricing tier | Product |
| **Incumbent Lock-In (Jobber, Housecall Pro)** | High - Switching costs and data migration friction | Build one-click CSV import, Google Calendar sync, migrate cards via Stripe network tokens | Eng |
| **Feature Creep** | Medium - Risk of building too much too fast | Focus ruthlessly on dispatch, quotes, payments; integrate (don't build) the rest | Product |
| **Stripe Account Setup Friction** | Medium - Operators may struggle with Stripe onboarding | Offer white-glove Stripe setup, allow cash/check tracking without Stripe | GTM |
| **Pilot Recruitment** | High - Need 20 committed paying pilots by Feb | Partner with detailing suppliers, leverage creator channels, offer early-bird discount ($39/mo) | GTM |
| **Routing Accuracy** | Medium - Bad routes will kill the value prop | Shadow 5 operators pre-launch, validate routing algorithm, offer manual override | Eng |

---

## What We're NOT Doing

**Important:** We're being disciplined about scope to ship fast and validate PMF.

- ❌ **Full Accounting/Bookkeeping** - QuickBooks export only; not building a full accounting system
- ❌ **Marketing Automation** - No email campaigns or social media scheduling in V1; focus on operational workflows
- ❌ **Advanced Fleet Management** - No GPS tracking, fuel management, or vehicle maintenance tracking in V1
- ❌ **Native Integrations Beyond Core** - Will use Zapier/Make for non-essential integrations (Mailchimp, HubSpot, etc.)
- ❌ **Multi-Vertical Expansion in Year 1** - Detailers only; mobile mechanics in 2026 after churn stabilizes
- ❌ **Custom Branding/White-Label (Enterprise)** - Basic branded booking pages only; no full white-label platform yet
- ❌ **Marketplace Features** - Not building a customer marketplace or lead generation platform in V1

---

## Go-To-Market Timeline

### Q1 2025 - Validation
- **Week 1-4:** Build validation MVP (booking + deposits + payments)
- **Week 5-8:** Recruit 20 paid pilots ($39-49/mo early-bird pricing)
  - Channels: Detailing Facebook groups, supplier partnerships, creator rev-share deals
- **Week 9-12:** Shadow 5 operators, measure drive time reduction and job capacity increase

### Q2 2025 - V1 Launch Prep
- **Month 3-4:** Complete V1 feature set (routing, messaging, CRM)
- **Month 5:** Closed beta with 50 additional customers
- **Month 6:** Public launch with SEO utilities (price calculator, scheduler templates)

### Q3 2025 - Scale
- **Month 7-9:** Launch V2 features (tech app, dynamic pricing, analytics)
- **Partnerships:** Activate supplier bundles (chemical distributors, tool vans)
- **Referral Program:** Launch referral incentives on branded booking pages

### Q4 2025 - Optimize
- **Focus:** Reduce churn <2%, increase ARPU to $120-150
- **Prep for 2026:** Begin mobile mechanics beta testing

---

## Decision Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2025-11-09 | Start with detailers, not mechanics | Detailers have simpler service catalog, less inventory complexity; faster to PMF |
| 2025-11-09 | Lead with routing + deposits, not just scheduling | Differentiation vs. Calendly/Square; core value prop is operational efficiency |
| 2025-11-09 | Build validation MVP before full V1 | Sell-first approach; validate willingness to pay and measure impact before full build |
| 2025-11-09 | Target $49-$99 pricing (not $29) | Avoid competing on price with incumbents; emphasize ROI (save 2-4 hrs/day = $50-100/day) |
| 2025-11-09 | React Native for tech app (not native iOS/Android) | Faster development, shared codebase, sufficient performance for this use case |

---

## Feedback and Questions

- **Q: Why not launch with mobile mechanics from day 1?**
  A: Mechanics have more complex inventory, parts sourcing, diagnostic tools. Detailers are a simpler wedge to validate core platform.

- **Q: What if routing doesn't deliver the promised savings?**
  A: We'll shadow operators pre-launch to validate algorithm. If routing isn't the key differentiator, we pivot to deposit/payment flows and quote automation as primary value props.

- **Q: How do we compete with free tools (Google Calendar, Square)?**
  A: We don't compete with free—we sell ROI. +1 job/day at $100 avg = $2,000-3,000/mo in additional revenue. Our $99/mo fee pays for itself if we save just 1 hour/week.

---

## Revision History

| Date | Changes | Updated By |
|------|---------|------------|
| 2025-11-09 | Initial 2025 roadmap created based on Auto Services SaaS Summary | Product Team |
