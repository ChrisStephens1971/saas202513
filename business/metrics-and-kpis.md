# Auto Services Platform - Business Metrics & KPIs

**Owner:** Product & Business Team
**Last Updated:** 2025-11-09
**Status:** Draft
**Review Frequency:** Weekly (operational), Monthly (strategic)

---

## Table of Contents

1. [Overview](#overview)
2. [North Star Metric](#north-star-metric)
3. [Core Product Metrics](#core-product-metrics)
4. [Financial Metrics](#financial-metrics)
5. [Customer Success Metrics](#customer-success-metrics)
6. [Operational Efficiency Metrics](#operational-efficiency-metrics)
7. [Go-to-Market Metrics](#go-to-market-metrics)
8. [Dashboard & Reporting](#dashboard--reporting)
9. [Targets by Quarter](#targets-by-quarter)

---

## Overview

### Purpose

This document defines the key metrics used to measure business performance, product-market fit, and operational efficiency for the Auto Services Platform. Metrics are organized by category and aligned with company OKRs.

### Measurement Philosophy

1. **Lead with outcomes, not outputs:** Focus on customer impact (e.g., "reduced no-shows") vs. features shipped
2. **Measure what matters:** Prioritize metrics that drive business decisions
3. **Keep it simple:** Track 5-7 core metrics per category; avoid metric overload
4. **Review regularly:** Weekly operational reviews, monthly strategic reviews

---

## North Star Metric

### Definition

**Net Revenue Retention (NRR)**

Net Revenue Retention measures revenue growth from existing customers (expansion + retention - churn). A healthy SaaS business has NRR >100%, meaning existing customers generate more revenue over time even without new customer acquisition.

### Why This Metric?

- **Validates PMF:** High NRR (>110%) indicates strong product-market fit
- **Predicts growth:** Customers expand usage (more techs, payment volume) as they see value
- **Reduces CAC dependency:** Growing revenue from existing base reduces pressure on new acquisition

### Target

| Period | Target NRR | Status |
|--------|-----------|--------|
| **Q2 2025** | 100% (baseline) | 🟡 Establishing baseline |
| **Q3 2025** | 105% | 🟡 Growth phase |
| **Q4 2025** | 110% | 🟢 PMF validated |
| **2026** | >120% | 🎯 Scale phase |

### Calculation

```
NRR = (Starting MRR + Expansion MRR - Churned MRR - Contraction MRR) / Starting MRR

Example (Q4 2025):
- Starting MRR (Oct 1): $50,000
- Expansion MRR: +$8,000 (customers upgrading to Teams plan, payment volume growth)
- Churned MRR: -$1,000 (2% monthly churn)
- Contraction MRR: $0 (no downgrades)
- Ending MRR (Dec 31): $57,000

NRR = ($50,000 + $8,000 - $1,000 - $0) / $50,000 = 114%
```

---

## Core Product Metrics

These metrics measure product usage and validate core value propositions.

---

### 1. Booking Conversion Rate

**Definition:** % of visitors to booking pages who complete a booking (deposit paid)

**Why It Matters:** Validates ease of self-service booking; low conversion = UX issues or pricing concerns

**Target:** ≥45% (industry avg: ~30%)

**Calculation:**
```
Booking Conversion = (Completed Bookings / Unique Visitors to Booking Page) × 100

Example:
- Visitors: 1,000
- Completed Bookings: 470
- Conversion: 47%
```

**Benchmarks:**
- 30-35%: Below average (investigate UX, pricing)
- 40-45%: Good (on track)
- 50%+: Excellent (optimize for scale)

**Dashboard View:**
- Weekly trend chart
- Breakdown by service type (Basic Detail vs. Premium)
- Mobile vs. desktop conversion

---

### 2. No-Show Rate (with Deposits)

**Definition:** % of confirmed bookings where customer doesn't show up (despite deposit paid)

**Why It Matters:** Core value prop is reducing no-shows via deposit-first booking; this proves ROI

**Target:** ≤3% (industry avg without deposits: ~15-20%)

**Calculation:**
```
No-Show Rate = (No-Shows / Total Confirmed Bookings) × 100

Example:
- Confirmed Bookings: 500
- No-Shows: 12
- No-Show Rate: 2.4%
```

**Benchmarks:**
- <2%: Excellent (deposit working)
- 3-5%: Good (monitor)
- >5%: Poor (investigate deposit amount, reminder timing)

**Impact Calculation:**
```
Monthly Revenue Saved = (Baseline No-Show Rate - Current No-Show Rate) × Avg Job Value × Monthly Jobs

Example (Solo Detailer):
- Baseline: 15% no-shows (industry avg)
- Current: 3% (with platform)
- Avg Job Value: $120
- Monthly Jobs: 100
- Revenue Saved: (15% - 3%) × $120 × 100 = $1,440/mo
```

---

### 3. Route Utilization (Service Time vs. Drive Time)

**Definition:** % of working hours spent on service (revenue-generating) vs. drive time (non-revenue)

**Why It Matters:** Core value prop is optimizing routes to reduce drive time; proves operational efficiency

**Target:** ≥80% service time (industry avg: ~50-60%)

**Calculation:**
```
Route Utilization = (Total Service Time / Total Working Time) × 100

Example (8-hour workday):
- Service Time: 6.5 hours (4 jobs × 1.5 hours avg)
- Drive Time: 1.0 hour
- Break Time: 0.5 hours
- Route Utilization: (6.5 / 8) × 100 = 81.25%
```

**Benchmarks:**
- <70%: Poor (too much drive time)
- 70-80%: Good (efficient routing)
- >80%: Excellent (optimal utilization)

**Impact Calculation:**
```
Additional Jobs Enabled = (Improved Utilization - Baseline) × Workday Hours / Avg Job Duration

Example:
- Baseline: 60% utilization = 4.8 hours service time
- Improved: 80% utilization = 6.4 hours service time
- Additional Service Time: 1.6 hours
- Avg Job Duration: 1.5 hours
- Additional Jobs: 1.6 / 1.5 ≈ +1 job/day
```

---

### 4. Self-Scheduled Jobs

**Definition:** % of jobs booked directly by customers (vs. operator manually entering)

**Why It Matters:** Reduces operator admin time; validates customer willingness to self-serve

**Target:** ≥60%

**Calculation:**
```
Self-Scheduled Rate = (Self-Scheduled Jobs / Total Jobs) × 100

Example:
- Total Jobs: 200
- Self-Scheduled: 130
- Manual Entry: 70
- Self-Scheduled Rate: 65%
```

**Benchmarks:**
- <50%: Low (improve booking page visibility, UX)
- 50-70%: Good (on track)
- >70%: Excellent (customers prefer self-service)

---

### 5. Payment Attach Rate

**Definition:** % of jobs processed through platform payments (vs. cash/check tracked manually)

**Why It Matters:** Payment fees drive revenue expansion; high attach = high ARPU

**Target:** ≥70% (stretch: 80%)

**Calculation:**
```
Payment Attach Rate = (Jobs Paid via Platform / Total Jobs) × 100

Example:
- Total Jobs: 200
- Platform Payments: 150
- Cash/Check: 50
- Payment Attach: 75%
```

**Impact on ARPU:**
```
Effective ARPU = Subscription Fee + (Payment Volume × Platform Fee %)

Example (Pro Plan at $99/mo):
- Jobs/Month: 100
- Avg Job Value: $120
- Payment Attach: 75%
- Payment Volume: 100 × $120 × 0.75 = $9,000
- Platform Fee: 1.5%
- Payment Revenue: $9,000 × 1.5% = $135
- Effective ARPU: $99 + $135 = $234/mo (2.4x subscription alone)
```

---

## Financial Metrics

### 1. Monthly Recurring Revenue (MRR)

**Definition:** Predictable monthly revenue from subscriptions and payment fees

**Target:** See quarterly targets below

**Calculation:**
```
MRR = Subscription MRR + Payment Fee MRR

Subscription MRR = Σ(Active Customers × Plan Price)
Payment Fee MRR = Σ(Monthly Payment Volume × Platform Fee %)

Example (Q4 2025):
- Customers: 840 (avg)
- Avg Plan Price: $90/mo (mix of Starter $49, Pro $99, Teams $149)
- Subscription MRR: 840 × $90 = $75,600

- Avg Payment Volume per Customer: $12,000/mo
- Platform Fee: 1.5%
- Payment Fee MRR: 840 × $12,000 × 0.015 = $151,200

Total MRR: $75,600 + $151,200 = $226,800
```

---

### 2. Annual Recurring Revenue (ARR)

**Definition:** Annualized MRR

**Target:** $2.0-2.7M by end of 2025

**Calculation:**
```
ARR = MRR × 12

Example (Dec 2025):
- MRR: $226,800
- ARR: $226,800 × 12 = $2,721,600
```

---

### 3. Customer Acquisition Cost (CAC)

**Definition:** Average cost to acquire one paying customer

**Target:** $80-200 (blended), optimize to <$100

**Calculation:**
```
CAC = Total Sales & Marketing Spend / New Customers Acquired

Example (Q3 2025):
- Marketing Spend: $15,000 (PPC, partnerships, SEO)
- Sales Spend: $5,000 (outreach, demos)
- Total S&M: $20,000
- New Customers: 200
- CAC: $20,000 / 200 = $100/customer
```

**CAC by Channel:**
| Channel | CAC | LTV/CAC Ratio | Priority |
|---------|-----|---------------|----------|
| **Referrals** | $0-50 | 99:1 | 🟢 High |
| **Supplier Partnerships** | $30-80 | 62:1 | 🟢 High |
| **SEO (Organic)** | $50-100 | 50:1 | 🟢 High |
| **Google Ads (PPC)** | $120-200 | 25:1 | 🟡 Medium |
| **Facebook Ads** | $100-180 | 28:1 | 🟡 Medium |

---

### 4. Customer Lifetime Value (LTV)

**Definition:** Total profit expected from a customer over their lifetime

**Target:** $4,950+ (at 2% churn, $99 ARPU)

**Calculation:**
```
LTV = (ARPU × Gross Margin) / Churn Rate

Example (Pro Plan, 2% churn):
- ARPU: $234/mo (subscription + payment fees)
- Gross Margin: 80% (SaaS subscription), 40% (payment fees) → Blended: 65%
- LTV = ($234 × 0.65) / 0.02 = $7,605

Conservative LTV (subscription only):
- ARPU: $99/mo
- Gross Margin: 85%
- LTV = ($99 × 0.85) / 0.02 = $4,207
```

**LTV:CAC Ratio:**
```
LTV:CAC = $7,605 / $100 = 76:1 (Excellent - target is >3:1)
```

---

### 5. Gross Margin

**Definition:** Revenue minus cost of goods sold (COGS)

**Target:** 80-85% (SaaS subscription), 65-70% (blended with payment fees)

**Calculation:**
```
Gross Margin % = (Revenue - COGS) / Revenue × 100

COGS includes:
- Hosting costs (Azure)
- Third-party API costs (Twilio, Mapbox)
- Payment processing fees (Stripe)

Example (Monthly):
- Revenue: $226,800
- COGS:
  - Azure hosting: $8,000
  - Twilio SMS: $3,000
  - Mapbox API: $1,500
  - Stripe fees (2.9% + $0.30 on $10M payment volume): $29,000
  - Total COGS: $41,500
- Gross Profit: $226,800 - $41,500 = $185,300
- Gross Margin: ($185,300 / $226,800) × 100 = 81.7%
```

---

## Customer Success Metrics

### 1. Monthly Churn Rate

**Definition:** % of customers who cancel their subscription each month

**Target:** <2% (Q4 2025), <3% (Q2-Q3 2025)

**Calculation:**
```
Monthly Churn Rate = (Customers Churned / Starting Customers) × 100

Example:
- Starting Customers (Oct 1): 800
- Churned in October: 14
- Churn Rate: (14 / 800) × 100 = 1.75%
```

**Churn Drivers (to monitor):**
- Seasonality (winter slowdown for detailers)
- Lack of payment attachment (low ROI)
- Poor onboarding (setup time >30 min)
- Competitor migration

**Mitigation Strategies:**
- Seasonal pause option ($0/mo, keep data)
- Proactive check-ins at day 7, 30, 90
- White-glove onboarding for first 100 customers

---

### 2. Net Promoter Score (NPS)

**Definition:** Likelihood of customers to recommend the product (scale 0-10)

**Target:** ≥50 (Q2 2025), ≥60 (Q4 2025)

**Calculation:**
```
NPS = % Promoters (9-10) - % Detractors (0-6)

Example (100 responses):
- Promoters (9-10): 65
- Passives (7-8): 25
- Detractors (0-6): 10
- NPS: 65% - 10% = 55
```

**Survey Cadence:**
- Send NPS survey quarterly to all active customers
- Send after key milestones (day 30, 90, 180)

**NPS Benchmarks:**
- <0: Poor (major product issues)
- 0-30: Fair (room for improvement)
- 30-50: Good (solid product)
- 50-70: Excellent (strong PMF)
- >70: World-class

---

### 3. Customer Health Score

**Definition:** Composite score (0-100) indicating customer satisfaction and churn risk

**Calculation:**
```
Health Score = Weighted Average of:
- Product Usage (40%): Jobs created, logins, features used
- Payment Attachment (30%): % jobs paid via platform
- Support Tickets (15%): # of tickets, resolution time
- NPS (15%): Latest NPS score

Example:
- Usage Score: 85/100 (4 jobs/week, daily logins)
- Payment Score: 80/100 (75% payment attach)
- Support Score: 90/100 (1 ticket, resolved in 2 hours)
- NPS Score: 100/100 (rated 10/10)
- Health Score: (85×0.4) + (80×0.3) + (90×0.15) + (100×0.15) = 86.5/100
```

**Health Tiers:**
- 80-100: Healthy (low churn risk, expansion candidate)
- 60-79: At Risk (proactive outreach needed)
- <60: Churning (immediate intervention)

---

## Operational Efficiency Metrics

### 1. Setup Time (Time to First Booking)

**Definition:** Time from signup to first completed booking

**Target:** <30 minutes (median)

**Calculation:**
```
Setup Time = Timestamp of First Booking - Signup Timestamp

Example:
- Signup: 2025-06-01 10:00 AM
- First Booking Created: 2025-06-01 10:22 AM
- Setup Time: 22 minutes
```

**Benchmarks:**
- <15 min: Excellent (simple onboarding)
- 15-30 min: Good (on track)
- 30-60 min: Fair (some friction)
- >60 min: Poor (UX issues)

---

### 2. Support Ticket Volume & Resolution Time

**Definition:** # of support tickets per customer per month, avg resolution time

**Target:**
- Ticket Volume: <0.5 tickets/customer/month
- Resolution Time: <24 hours (median)

**Calculation:**
```
Tickets per Customer = Total Tickets / Active Customers

Resolution Time (Median) = Median(Ticket Closed Time - Ticket Created Time)

Example:
- Active Customers: 840
- Tickets in November: 320
- Tickets per Customer: 320 / 840 = 0.38

- Ticket Resolution Times: [2h, 4h, 6h, 12h, 18h, 24h, 48h]
- Median Resolution: 12 hours
```

**Ticket Categories (prioritize fixes):**
- Setup Issues (30%): Improve onboarding
- Payment Errors (20%): Improve Stripe integration
- Google Calendar Sync (15%): Improve sync reliability
- Feature Requests (20%): Prioritize roadmap
- General Questions (15%): Improve documentation

---

## Go-to-Market Metrics

### 1. Lead-to-Customer Conversion Rate

**Definition:** % of leads (trial signups, demo requests) that convert to paying customers

**Target:** ≥40% (from trial to paid)

**Calculation:**
```
Conversion Rate = (Paying Customers / Total Leads) × 100

Example:
- Free Trial Signups: 500
- Converted to Paid: 220
- Conversion Rate: 44%
```

---

### 2. Customer Payback Period

**Definition:** Months to recover CAC from customer revenue

**Target:** <6 months

**Calculation:**
```
Payback Period = CAC / (ARPU × Gross Margin)

Example:
- CAC: $100
- ARPU: $234/mo
- Gross Margin: 70%
- Gross Profit per Month: $234 × 0.70 = $163.80
- Payback Period: $100 / $163.80 = 0.61 months (~18 days)
```

---

## Dashboard & Reporting

### Weekly Operational Dashboard

**Metrics:**
- New customers this week
- Churn this week
- MRR growth
- Support ticket volume
- NPS (latest survey results)

**Owner:** Product team
**Distribution:** Slack #metrics channel, Monday morning

---

### Monthly Strategic Dashboard

**Metrics:**
- ARR trend (vs. target)
- NRR
- CAC & LTV
- Churn rate
- Product metrics (booking conversion, no-show rate, route utilization)

**Owner:** CEO / Product lead
**Distribution:** Board deck, investor updates

---

### Customer Success Dashboard

**Metrics (per customer):**
- Health score
- Jobs created this month
- Payment attach rate
- Last login
- Support tickets

**Owner:** Customer Success team
**Use Case:** Identify at-risk customers, expansion opportunities

---

## Targets by Quarter

### Q1 2025 (Validation MVP)

| Metric | Target | Status |
|--------|--------|--------|
| **Paid Customers** | 20 pilots | 🎯 |
| **MRR** | $1,500 | 🎯 |
| **Monthly Churn** | 5-6% (acceptable for pilots) | 🟡 |
| **Payment Attach Rate** | 70% | 🎯 |
| **Setup Time** | <30 min | 🎯 |
| **No-Show Rate** | ≤5% | 🎯 |

---

### Q2 2025 (V1 Launch)

| Metric | Target | Status |
|--------|--------|--------|
| **Paid Customers** | 100 | 🎯 |
| **MRR** | $7,500 | 🎯 |
| **ARR** | $90K | 🎯 |
| **Monthly Churn** | 3-4% | 🎯 |
| **Payment Attach Rate** | 70% | 🎯 |
| **Booking Conversion** | ≥45% | 🎯 |
| **Route Utilization** | ≥75% | 🎯 |
| **NPS** | ≥50 | 🎯 |
| **CAC** | <$150 | 🎯 |
| **LTV** | $3,500+ | 🎯 |
| **NRR** | 100% (baseline) | 🎯 |

---

### Q3 2025 (Scale)

| Metric | Target | Status |
|--------|--------|--------|
| **Paid Customers** | 400 | 🎯 |
| **MRR** | $30,000 | 🎯 |
| **ARR** | $360K | 🎯 |
| **Monthly Churn** | 2-3% | 🎯 |
| **Payment Attach Rate** | 75% | 🎯 |
| **Booking Conversion** | ≥50% | 🎯 |
| **Route Utilization** | ≥80% | 🎯 |
| **Self-Scheduled Jobs** | ≥65% | 🎯 |
| **NPS** | ≥55 | 🎯 |
| **CAC** | <$120 | 🎯 |
| **LTV** | $4,500+ | 🎯 |
| **NRR** | 105% | 🎯 |

---

### Q4 2025 (PMF Validation)

| Metric | Target | Status |
|--------|--------|--------|
| **Paid Customers** | 840-1,440 | 🎯 |
| **MRR** | $63K-108K | 🎯 |
| **ARR** | $756K-1.3M | 🎯 |
| **Monthly Churn** | <2% | 🎯 |
| **Payment Attach Rate** | 80% | 🎯 |
| **Booking Conversion** | ≥55% | 🎯 |
| **No-Show Rate** | ≤2% | 🎯 |
| **Route Utilization** | ≥85% | 🎯 |
| **Self-Scheduled Jobs** | ≥70% | 🎯 |
| **NPS** | ≥60 | 🎯 |
| **CAC** | <$100 | 🎯 |
| **LTV** | $4,950+ | 🎯 |
| **NRR** | >110% (PMF validated) | 🎯 |

---

## Appendix

### Related Documents

- **Product Roadmap:** `product/roadmap/2025-product-roadmap.md`
- **Business Plan:** `project-brief/Auto_Services_SaaS_Summary.pdf`
- **Pricing Strategy:** `business/pricing-model.md` (to be created)
- **OKRs:** `business/okrs/` (to be created)

---

**End of Metrics & KPIs Document**
