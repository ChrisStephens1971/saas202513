# Sprint 1 - Validation MVP

**Sprint Duration:** Dec 1, 2024 - Jan 31, 2025 (8 weeks)
**Sprint Goal:** Launch Validation MVP to test core value proposition with 20 paid pilots
**Status:** Planning

---

## Sprint Goal

Build and launch a minimal viable product that validates our core value proposition: **"Reduce no-shows through deposit-first booking and accelerate cash flow with integrated payments."**

The Validation MVP must enable mobile detailers to:
1. Accept subscription payments ($39-49/mo early-bird pricing)
2. Create and send quotes to customers
3. Collect 50% deposits on all bookings
4. Sync bookings with Google Calendar
5. Send automated SMS confirmations
6. Track payment status (paid/unpaid)

**Success Criteria:**
- ≥20 paid pilots by Jan 31, 2025
- Setup time <30 minutes
- ≥70% payment attach rate (deposits collected on ≥70% of bookings)
- No-show rate ≤5% (baseline measurement for future comparison)

---

## Sprint Capacity

**Available Days:** 8 weeks (Dec 1 - Jan 31)
**Team Size:** 2-3 developers (full-stack)
**Capacity:** ~320-480 hours (40-60 hours/week)
**Commitments/Time Off:** Holiday break (Dec 23 - Jan 2, ~10 days reduced capacity)

**Adjusted Capacity:** ~280-400 hours

---

## Sprint Backlog

### High Priority (Must Complete)

| Story | Description | Estimate | Assignee | Status | Notes |
|-------|-------------|----------|----------|--------|-------|
| US-001 | Project setup: Azure infrastructure, database, CI/CD | L (40h) | Eng | 📋 Todo | Foundation |
| US-002 | Stripe subscription checkout | M (24h) | Eng | 📋 Todo | Revenue critical |
| US-003 | Basic booking calendar (time slot selection) | L (32h) | Eng | 📋 Todo | Core feature |
| US-004 | Deposit collection (50% upfront via Stripe) | M (24h) | Eng | 📋 Todo | No-show prevention |
| US-005 | Google Calendar import (one-way sync) | M (20h) | Eng | 📋 Todo | Migration path |
| US-006 | SMS booking confirmation (Twilio integration) | S (16h) | Eng | 📋 Todo | Customer communication |
| US-007 | Simple quote builder (packages + custom) | M (24h) | Eng | 📋 Todo | Sales process |
| US-008 | Basic payment tracking (paid/unpaid invoices) | S (16h) | Eng | 📋 Todo | Cash flow visibility |

**Total High Priority:** ~196 hours

---

### Medium Priority (Should Complete)

| Story | Description | Estimate | Assignee | Status | Notes |
|-------|-------------|----------|----------|--------|-------|
| US-009 | Operator dashboard (jobs, revenue, customers) | M (20h) | Eng | 📋 Todo | UX improvement |
| US-010 | Customer database (name, phone, email, address) | S (12h) | Eng | 📋 Todo | Foundation for CRM |
| US-011 | Branded booking pages (subdomain routing) | M (24h) | Eng | 📋 Todo | Customer acquisition |
| US-012 | Basic auth & tenant management | M (20h) | Eng | 📋 Todo | Multi-tenant foundation |

**Total Medium Priority:** ~76 hours

**Total Committed (High + Medium):** ~272 hours (fits within capacity)

---

### Low Priority (Nice to Have)

| Story | Description | Estimate | Assignee | Status | Notes |
|-------|-------------|----------|----------|--------|-------|
| US-013 | Email notifications (SendGrid) | S (12h) | Eng | 📋 Todo | Backup to SMS |
| US-014 | Vehicle database (make, model, year) | S (8h) | Eng | 📋 Todo | Quote accuracy |
| US-015 | Basic analytics (jobs this week, revenue) | S (12h) | Eng | 📋 Todo | Operator insights |

**Total Low Priority:** ~32 hours (only if time permits)

---

**Story Status Legend:**
- 📋 Todo
- 🏗️ In Progress
- 👀 In Review
- ✅ Done
- ❌ Blocked

---

## Technical Debt / Maintenance

Items that need attention but aren't new features:

- [ ] Set up Azure monitoring (Application Insights)
- [ ] Configure automated backups for PostgreSQL
- [ ] Set up error tracking (Sentry or similar)
- [ ] Create deployment runbook documentation

---

## Detailed User Stories

### US-001: Project Setup - Azure Infrastructure, Database, CI/CD

**Epic:** Infrastructure
**Priority:** P0
**Estimate:** L (40 hours)
**Status:** 📋 Todo

**User Story:**
As a **developer**
I want **a fully configured Azure infrastructure with PostgreSQL, Redis, and CI/CD pipelines**
So that **the team can develop and deploy the application efficiently**

**Acceptance Criteria:**
- [ ] Azure Container Apps provisioned (dev, staging, production)
- [ ] PostgreSQL 16 database created on Azure Database for PostgreSQL
- [ ] Redis cache provisioned on Azure Cache for Redis
- [ ] Azure Key Vault configured for secrets management
- [ ] GitHub Actions CI/CD pipeline deploys to staging on push to `develop` branch
- [ ] Database migrations run automatically on deployment
- [ ] Environment variables loaded from Key Vault
- [ ] Health check endpoint returns 200 OK

**Implementation Notes:**
- Use Bicep templates from `infrastructure/bicep/`
- Follow Verdaio naming standard (e.g., `app-vrd-202513-dev-eus2-01`)
- Configure multi-tenant database with RLS policies
- Set up Stripe test mode for dev/staging, production mode for prod

**See:** `technical/infrastructure/AZURE-DEPLOYMENT-GUIDE.md`

---

### US-002: Stripe Subscription Checkout

**Epic:** Payments
**Priority:** P0
**Estimate:** M (24 hours)
**Status:** 📋 Todo

**User Story:**
As a **mobile detailer**
I want **to sign up and pay for a subscription ($39-49/mo) via Stripe**
So that **I can access the platform and start managing my business**

**Acceptance Criteria:**
- [ ] Stripe Checkout session created for subscription signup
- [ ] Two pricing plans: Starter ($49/mo) and Early-Bird ($39/mo for first 50 pilots)
- [ ] Successful payment creates tenant account in database
- [ ] Tenant assigned unique subdomain (e.g., `mikesdetailing.autoservices.app`)
- [ ] Subscription status synced via Stripe webhooks (active, past_due, canceled)
- [ ] Failed payments trigger email notification
- [ ] Subscription can be canceled from dashboard (downgrades to read-only mode)

**Implementation Notes:**
- Use Stripe Checkout (hosted page) for fast implementation
- Stripe Customer ID stored in `tenants` table
- Webhook endpoint: `POST /api/webhooks/stripe`
- Handle events: `checkout.session.completed`, `invoice.payment_failed`, `customer.subscription.deleted`

**Technical Dependencies:**
- Stripe Connect account approved (apply by Dec 1)

---

### US-003: Basic Booking Calendar (Time Slot Selection)

**Epic:** Smart Booking
**Priority:** P0
**Estimate:** L (32 hours)
**Status:** 📋 Todo

**User Story:**
As a **customer**
I want **to view available time slots and select a date/time for my detailing service**
So that **I can book an appointment without calling the business**

**Acceptance Criteria:**
- [ ] Calendar view displays available time slots (week view)
- [ ] Operator configures working hours (e.g., Mon-Sat 8am-6pm)
- [ ] Operator configures service duration (e.g., Basic Detail = 2 hours, Full Detail = 4 hours)
- [ ] System blocks unavailable times based on existing bookings
- [ ] Customer selects service type (Basic, Full, Premium)
- [ ] Customer selects date and time
- [ ] Booking form captures: name, phone, email, address, vehicle details
- [ ] Booking saved to database with status "pending" (until deposit paid)
- [ ] Confirmation screen shows booking details and deposit amount

**Implementation Notes:**
- Use React Big Calendar or FullCalendar for calendar UI
- Backend: Express endpoint `POST /api/bookings`
- Database table: `bookings` (tenant_id, customer_id, service_type, start_time, end_time, status, deposit_amount, total_amount)
- Calculate available slots dynamically based on working hours and existing bookings

**Design Reference:**
- Calendly-style time slot picker
- Mobile-responsive (most customers book on mobile)

---

### US-004: Deposit Collection (50% Upfront via Stripe)

**Epic:** Payments
**Priority:** P0
**Estimate:** M (24 hours)
**Status:** 📋 Todo

**User Story:**
As a **mobile detailer**
I want **to require a 50% deposit on all bookings**
So that **I reduce no-shows from ~15% to <5%**

**Acceptance Criteria:**
- [ ] After customer selects time slot, they are taken to Stripe Checkout for deposit payment
- [ ] Deposit amount = 50% of total service price
- [ ] Stripe Checkout accepts card, Apple Pay, Google Pay
- [ ] Successful payment confirms booking and changes status to "confirmed"
- [ ] Failed payment shows error message and allows retry
- [ ] Stripe Payment Intent ID stored in `bookings` table
- [ ] Remaining balance (50%) marked as "due on completion"
- [ ] Operator can manually mark remaining balance as paid (cash option)

**Implementation Notes:**
- Use Stripe Checkout (one-time payment mode, not subscription)
- Payment Intent metadata includes: `tenant_id`, `booking_id`, `customer_id`
- Webhook event: `checkout.session.completed` → update booking status to "confirmed"
- Store card-on-file for future charges (remaining balance)

**Business Logic:**
- If customer is more than 30 min late, deposit forfeited (no-show fee)
- Operator can refund deposit from dashboard (Stripe Refund API)

---

### US-005: Google Calendar Import (One-Way Sync)

**Epic:** Integrations
**Priority:** P0
**Estimate:** M (20 hours)
**Status:** 📋 Todo

**User Story:**
As a **mobile detailer**
I want **to import my existing Google Calendar appointments**
So that **I don't have to manually re-enter my schedule and can avoid double-bookings**

**Acceptance Criteria:**
- [ ] Operator clicks "Import Google Calendar" button in dashboard
- [ ] OAuth flow authorizes access to Google Calendar
- [ ] System imports all events from the next 30 days
- [ ] Imported events block time slots on booking calendar
- [ ] Imported events marked as "external" (not created in platform)
- [ ] Sync runs every 15 minutes to pull new Google Calendar events
- [ ] Operator can disconnect Google Calendar integration

**Implementation Notes:**
- Google Calendar API (OAuth 2.0)
- Use `google-auth-library` npm package
- Store OAuth refresh token in `tenants` table (encrypted)
- Cron job: Poll Google Calendar API every 15 min for new/updated events
- Map Google Calendar events to `bookings` table with `source = 'google_calendar'`

**Edge Cases:**
- Handle all-day events (block entire day)
- Handle recurring events (import individual instances, not series)
- Handle deleted events (remove from platform)

---

### US-006: SMS Booking Confirmation (Twilio Integration)

**Epic:** Messaging
**Priority:** P0
**Estimate:** S (16 hours)
**Status:** 📋 Todo

**User Story:**
As a **customer**
I want **to receive an SMS confirmation immediately after booking**
So that **I have proof of my appointment and know when the tech will arrive**

**Acceptance Criteria:**
- [ ] SMS sent to customer immediately after successful deposit payment
- [ ] SMS includes: business name, service type, date/time, address, total amount
- [ ] SMS includes link to view/cancel booking (e.g., `autoservices.app/bookings/{id}`)
- [ ] SMS sender ID shows business name (if supported by Twilio)
- [ ] Failed SMS logged (customer phone number invalid or Twilio error)
- [ ] SMS includes opt-out language: "Reply STOP to unsubscribe"

**Message Template:**
```
Hi {CustomerName}! Your {ServiceType} is confirmed for {Date} at {Time}.

Address: {Address}
Total: ${TotalAmount} (${DepositPaid} paid, ${Remaining} due on completion)

View/Cancel: {BookingLink}

- {BusinessName}
Reply STOP to unsubscribe.
```

**Implementation Notes:**
- Use Twilio Programmable Messaging API
- Store Twilio Account SID and Auth Token in Azure Key Vault
- Database table: `messages` (tenant_id, customer_id, booking_id, message_body, status, sent_at)
- Use message templates stored in database (`message_templates` table)

**Cost Consideration:**
- Twilio SMS: ~$0.0075/message (US)
- Estimate 500 messages/mo per operator = ~$3.75/mo per operator

---

### US-007: Simple Quote Builder (Packages + Custom)

**Epic:** Quote Builder
**Priority:** P0
**Estimate:** M (24 hours)
**Status:** 📋 Todo

**User Story:**
As a **mobile detailer**
I want **to create and send professional quotes to potential customers**
So that **I can standardize pricing and convert leads to bookings faster**

**Acceptance Criteria:**
- [ ] Operator can create quote from dashboard
- [ ] Pre-configured service packages (Basic Detail $80, Full Detail $150, Premium $250)
- [ ] Operator can add custom line items (e.g., Headlight Restoration +$40)
- [ ] Operator can adjust total price manually
- [ ] Quote includes customer contact info (name, phone, email)
- [ ] Quote sent via SMS with link to view and accept
- [ ] Customer clicks link → views quote details → clicks "Accept & Book" → taken to booking calendar
- [ ] Accepted quote auto-populates booking form with services and price
- [ ] Operator can track quote status (sent, viewed, accepted, declined, expired)

**Quote Link Example:**
```
Hi {CustomerName}! Here's your quote for {ServiceType}:

Total: ${QuoteAmount}

View & Book: {QuoteLink}

Valid for 7 days. Questions? Reply to this message.

- {BusinessName}
```

**Implementation Notes:**
- Database table: `quotes` (tenant_id, customer_id, services, total_amount, status, expires_at)
- Database table: `service_packages` (tenant_id, name, description, price, duration)
- Quote page: Public-facing page at `/quotes/{quote_id}` (no auth required)
- "Accept & Book" button redirects to `/book?quote={quote_id}` with quote details pre-filled

**Metrics:**
- Track quote-to-booking conversion rate (# accepted / # sent)

---

### US-008: Basic Payment Tracking (Paid/Unpaid Invoices)

**Epic:** Payments
**Priority:** P0
**Estimate:** S (16 hours)
**Status:** 📋 Todo

**User Story:**
As a **mobile detailer**
I want **to see which jobs are paid vs. unpaid at a glance**
So that **I can follow up on outstanding payments and improve cash flow**

**Acceptance Criteria:**
- [ ] Dashboard shows list of jobs with payment status (Paid, Partially Paid, Unpaid, Overdue)
- [ ] Paid = 100% collected (deposit + remaining balance)
- [ ] Partially Paid = Deposit collected, balance due
- [ ] Unpaid = No payment collected (shouldn't happen with deposit-first flow)
- [ ] Overdue = Job completed >7 days ago, remaining balance not paid
- [ ] Operator can click "Mark as Paid" to manually record cash/check payment
- [ ] Operator can send payment reminder SMS to customers with unpaid balance
- [ ] Total outstanding balance displayed prominently on dashboard

**Implementation Notes:**
- Calculate payment status dynamically based on `payments` table
- Dashboard query:
  ```sql
  SELECT
    bookings.id,
    bookings.total_amount,
    COALESCE(SUM(payments.amount), 0) AS amount_paid,
    bookings.total_amount - COALESCE(SUM(payments.amount), 0) AS balance_due,
    CASE
      WHEN COALESCE(SUM(payments.amount), 0) >= bookings.total_amount THEN 'Paid'
      WHEN COALESCE(SUM(payments.amount), 0) > 0 THEN 'Partially Paid'
      WHEN bookings.completed_at < NOW() - INTERVAL '7 days' THEN 'Overdue'
      ELSE 'Unpaid'
    END AS payment_status
  FROM bookings
  LEFT JOIN payments ON payments.booking_id = bookings.id
  WHERE bookings.tenant_id = ?
  GROUP BY bookings.id
  ```

**Payment Reminder Template:**
```
Hi {CustomerName}! Thanks for choosing {BusinessName}.

You have an outstanding balance of ${BalanceDue} for your {ServiceType} on {Date}.

Pay now: {PaymentLink}

Questions? Reply to this message.
```

---

### US-009: Operator Dashboard (Jobs, Revenue, Customers)

**Epic:** Dashboard
**Priority:** P1
**Estimate:** M (20 hours)
**Status:** 📋 Todo

**User Story:**
As a **mobile detailer**
I want **a simple dashboard that shows today's jobs, weekly revenue, and customer count**
So that **I can quickly understand my business performance**

**Acceptance Criteria:**
- [ ] Dashboard displays key metrics:
  - Today's jobs (list with time, customer name, service, address)
  - This week's revenue (total collected)
  - Total customers (unique customers served)
  - Outstanding balance (unpaid invoices)
- [ ] Quick actions:
  - Create new booking
  - Send quote
  - View calendar
- [ ] Recent activity feed (last 10 bookings/quotes)
- [ ] Mobile-responsive design

**Implementation Notes:**
- Use chart library (Recharts or Chart.js) for revenue graph
- Real-time updates using React Query
- Dashboard endpoint: `GET /api/dashboard/metrics`

---

### US-010: Customer Database (Name, Phone, Email, Address)

**Epic:** CRM
**Priority:** P1
**Estimate:** S (12 hours)
**Status:** 📋 Todo

**User Story:**
As a **mobile detailer**
I want **a database of all my customers with contact info and addresses**
So that **I can quickly look up customer details and track repeat business**

**Acceptance Criteria:**
- [ ] Customers automatically created when booking is made
- [ ] Customer record includes: name, phone, email, primary address
- [ ] Customers page displays searchable/filterable list
- [ ] Search by name, phone, or email
- [ ] Click customer to view profile (bookings history, total spent, last service date)
- [ ] Operator can manually add customer (for walk-ins or phone bookings)
- [ ] Operator can edit customer details
- [ ] Duplicate detection (same phone number or email warns operator)

**Implementation Notes:**
- Database table: `customers` (tenant_id, name, phone, email, address, created_at, last_booking_at, total_spent)
- Aggregate queries for `total_spent` and `last_booking_at`:
  ```sql
  UPDATE customers SET
    total_spent = (SELECT SUM(total_amount) FROM bookings WHERE customer_id = customers.id),
    last_booking_at = (SELECT MAX(start_time) FROM bookings WHERE customer_id = customers.id)
  WHERE id = ?
  ```

---

### US-011: Branded Booking Pages (Subdomain Routing)

**Epic:** Customer Acquisition
**Priority:** P1
**Estimate:** M (24 hours)
**Status:** 📋 Todo

**User Story:**
As a **mobile detailer**
I want **a branded booking page at my own subdomain (e.g., mikesdetailing.autoservices.app)**
So that **I can share a professional link with customers for self-service bookings**

**Acceptance Criteria:**
- [ ] Each tenant assigned unique subdomain upon signup (e.g., `{businessname}.autoservices.app`)
- [ ] Booking page displays business name, logo (optional), and tagline
- [ ] Customer sees service packages with descriptions and prices
- [ ] Customer can book directly without operator involvement
- [ ] Booking page is mobile-responsive
- [ ] Subdomain configurable by operator (e.g., change from `mikes-detailing` to `mikesautodetail`)
- [ ] Custom domain support (future: `book.mikesdetailing.com`)

**Implementation Notes:**
- Use Next.js middleware to detect subdomain and load tenant data
- Example route: `app/[subdomain]/book/page.tsx`
- Tenant lookup by subdomain:
  ```sql
  SELECT * FROM tenants WHERE subdomain = ?
  ```
- Fallback to main domain if subdomain not found (404 page)

**SEO Considerations:**
- Each booking page has unique `<title>` and `<meta description>` tags
- Schema.org LocalBusiness markup for SEO

---

### US-012: Basic Auth & Tenant Management

**Epic:** Infrastructure
**Priority:** P1
**Estimate:** M (20 hours)
**Status:** 📋 Todo

**User Story:**
As a **mobile detailer**
I want **to sign up, log in, and manage my account securely**
So that **my business data is protected and only I can access it**

**Acceptance Criteria:**
- [ ] Email/password signup and login
- [ ] Password hashing (bcrypt)
- [ ] JWT-based authentication
- [ ] Session expiration (7 days)
- [ ] Password reset via email (forgot password flow)
- [ ] Account settings page (update business name, email, phone)
- [ ] Multi-user support (future: add team members with roles)

**Implementation Notes:**
- Use `bcrypt` for password hashing
- Use `jsonwebtoken` for JWT generation
- Store JWT in httpOnly cookie (prevent XSS)
- Middleware: `requireAuth` checks JWT on protected routes
- Database table: `users` (tenant_id, email, password_hash, role, created_at)

**Security:**
- Rate limit login attempts (5 failed attempts = 15 min lockout)
- Password requirements: min 8 characters, 1 uppercase, 1 number

---

## Scope Changes

Document any stories added or removed during the sprint:

| Date | Change | Reason |
|------|--------|--------|
| (none yet) | - | - |

---

## Sprint Metrics

### Planned vs Actual
- **Planned:** 272 hours (High + Medium priority)
- **Completed:** (to be updated at sprint end)
- **Completion Rate:** (to be calculated)

### Velocity
- **Previous Sprint:** N/A (first sprint)
- **This Sprint:** (to be measured)
- **Trend:** Baseline

---

## Wins & Learnings

*(To be completed during sprint retrospective)*

### What Went Well
- (to be filled)

### What Could Be Improved
- (to be filled)

### Action Items for Next Sprint
- [ ] (to be filled)

---

## Sprint Review Notes

*(To be completed at end of sprint)*

**What We Shipped:**
- (to be filled)

**Demo Notes:**
- (to be filled)

**Feedback Received:**
- (to be filled)

---

## Links & References

- **Product Roadmap:** `product/roadmap/2025-product-roadmap.md`
- **V1 MVP PRD:** `product/PRDs/v1-mvp-auto-services-platform.md`
- **Auto Services SaaS Summary:** `project-brief/Auto_Services_SaaS_Summary.pdf`
- **Azure Deployment Guide:** `technical/infrastructure/AZURE-DEPLOYMENT-GUIDE.md`
- **GitHub Milestone:** (to be created)
- **Design Files:** (to be created in Figma)

---

## Next Steps After Sprint 1

1. **Pilot Recruitment (Week 9-12):** Recruit 20 paid pilots at $39-49/mo
2. **User Testing:** Shadow 5 operators to validate platform effectiveness
3. **Metrics Measurement:** Track no-show rate, payment attach rate, setup time
4. **Sprint 2 Planning:** Based on pilot feedback, prioritize V1 features (routing, messaging, advanced CRM)
