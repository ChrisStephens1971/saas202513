# Auto Services Platform - System Architecture

**Version:** 1.0
**Date:** 2025-11-09
**Status:** Draft
**Owner:** Engineering Team

---

## Table of Contents

1. [Overview](#overview)
2. [System Architecture](#system-architecture)
3. [Technology Stack](#technology-stack)
4. [Data Architecture](#data-architecture)
5. [Multi-Tenant Architecture](#multi-tenant-architecture)
6. [Third-Party Integrations](#third-party-integrations)
7. [Security & Compliance](#security--compliance)
8. [Scalability & Performance](#scalability--performance)
9. [DevOps & CI/CD](#devops--cicd)
10. [Monitoring & Observability](#monitoring--observability)

---

## Overview

### Product Summary

The Auto Services Platform is a multi-tenant SaaS solution for mobile auto detailers that centralizes booking, automates quotes, optimizes routing, and accelerates payments. The system must support:

- **Multi-tenancy:** Thousands of independent detailing businesses (tenants)
- **Real-time operations:** Booking, routing, messaging
- **Payment processing:** Stripe integration for deposits and invoices
- **High availability:** 99.9% uptime SLA
- **Mobile-first:** Customers and technicians primarily use mobile devices

### Architecture Principles

1. **Multi-Tenant by Design:** All data isolated by `tenant_id` with Row-Level Security (RLS)
2. **API-First:** RESTful API powers web, mobile, and third-party integrations
3. **Scalability:** Horizontal scaling via Azure Container Apps
4. **Security:** PCI DSS compliant (via Stripe), GDPR/CCPA ready
5. **Cost-Efficiency:** Serverless where possible, pay-per-use model
6. **Reliability:** Automated failover, backups, and monitoring

---

## System Architecture

### High-Level Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           Internet / Users                               │
└────────────────┬────────────────────────────────┬───────────────────────┘
                 │                                 │
                 │                                 │
        ┌────────▼─────────┐              ┌───────▼────────┐
        │  Customer Web    │              │ Operator Web   │
        │  (Booking Pages) │              │   Dashboard    │
        │                  │              │                │
        │  React (Next.js) │              │ React          │
        │  SSR             │              │ (Next.js)      │
        └────────┬─────────┘              └───────┬────────┘
                 │                                 │
                 └────────────┬────────────────────┘
                              │
                              │ HTTPS
                              │
                ┌─────────────▼──────────────┐
                │   Azure Front Door         │
                │   (CDN + WAF + DDoS)       │
                └─────────────┬──────────────┘
                              │
                              │
                ┌─────────────▼──────────────┐
                │  Azure Container Apps      │
                │  (Auto-scaling)            │
                │                            │
                │  ┌──────────────────────┐  │
                │  │  API Service         │  │
                │  │  Node.js (Express)   │  │
                │  │  REST API            │  │
                │  └──────────┬───────────┘  │
                └─────────────┼──────────────┘
                              │
          ┌───────────────────┼──────────────────────┐
          │                   │                      │
          │                   │                      │
  ┌───────▼────────┐  ┌──────▼──────┐      ┌────────▼────────┐
  │  PostgreSQL 16 │  │   Redis     │      │  Azure Blob     │
  │  (Azure DB)    │  │  (Cache)    │      │  Storage        │
  │                │  │             │      │  (Media)        │
  │  Multi-tenant  │  │  Sessions   │      │                 │
  │  with RLS      │  │  Rate Limit │      │  Photos/Videos  │
  └────────────────┘  └─────────────┘      └─────────────────┘
          │
          │
  ┌───────▼──────────────────────────────────────────────────┐
  │              Third-Party Services                         │
  │                                                            │
  │  ┌──────────┐  ┌──────────┐  ┌─────────────┐  ┌────────┐ │
  │  │  Stripe  │  │  Twilio  │  │   Mapbox    │  │ Google │ │
  │  │ Payments │  │   SMS    │  │  Routing    │  │Calendar│ │
  │  └──────────┘  └──────────┘  └─────────────┘  └────────┘ │
  │                                                            │
  └────────────────────────────────────────────────────────────┘
```

### Component Breakdown

#### 1. **Frontend Applications**

**Customer Booking Pages (Public)**
- **Tech:** Next.js (React) with Server-Side Rendering (SSR)
- **URL:** `{subdomain}.autoservices.app` (e.g., `mikesdetailing.autoservices.app`)
- **Purpose:** Customer-facing booking flow (select service → pick time → pay deposit)
- **Hosting:** Azure Static Web Apps or Container Apps

**Operator Dashboard (Authenticated)**
- **Tech:** React (Next.js)
- **URL:** `app.autoservices.app`
- **Purpose:** Operator management (view bookings, create quotes, track payments)
- **Hosting:** Azure Container Apps

---

#### 2. **API Service (Backend)**

**Technology:** Node.js with Express or Fastify
**Hosting:** Azure Container Apps (auto-scaling)
**Responsibilities:**
- RESTful API endpoints for CRUD operations
- Business logic (booking validation, route optimization, payment processing)
- Authentication & authorization (JWT)
- Webhook handlers (Stripe, Twilio, Google Calendar)
- Multi-tenant data isolation (inject `tenant_id` into all queries)

**Key API Routes:**
```
Authentication:
- POST /api/auth/signup
- POST /api/auth/login
- POST /api/auth/logout
- POST /api/auth/forgot-password

Bookings:
- GET    /api/bookings
- POST   /api/bookings
- GET    /api/bookings/:id
- PATCH  /api/bookings/:id
- DELETE /api/bookings/:id

Quotes:
- GET    /api/quotes
- POST   /api/quotes
- GET    /api/quotes/:id
- PATCH  /api/quotes/:id/accept

Customers:
- GET    /api/customers
- POST   /api/customers
- GET    /api/customers/:id
- PATCH  /api/customers/:id

Payments:
- POST   /api/payments/create-checkout-session
- POST   /api/payments/charge-card-on-file
- GET    /api/payments/:id

Routes:
- POST   /api/routes/optimize
- GET    /api/routes/:date

Messaging:
- POST   /api/messages/send
- GET    /api/messages
- GET    /api/messages/:id

Integrations:
- POST   /api/integrations/google-calendar/connect
- POST   /api/integrations/google-calendar/sync
- DELETE /api/integrations/google-calendar/disconnect

Webhooks:
- POST   /api/webhooks/stripe
- POST   /api/webhooks/twilio
- POST   /api/webhooks/google-calendar
```

---

#### 3. **Database (PostgreSQL 16)**

**Hosting:** Azure Database for PostgreSQL (Flexible Server)
**Configuration:**
- **Multi-tenant:** All tables include `tenant_id` column
- **Row-Level Security (RLS):** Enforced at database level
- **Backups:** Automated daily backups with 30-day retention
- **Replication:** Read replicas for reporting queries (optional, post-PMF)

**Database Schema:** See [Data Architecture](#data-architecture) section

---

#### 4. **Cache (Redis)**

**Hosting:** Azure Cache for Redis
**Use Cases:**
- **Session storage:** Store JWT tokens and user sessions
- **Rate limiting:** Prevent API abuse (per-tenant rate limits)
- **Query caching:** Cache frequently accessed data (service packages, tenant settings)
- **Job queues:** Background jobs (send SMS, sync Google Calendar)

---

#### 5. **Blob Storage (Azure Blob Storage)**

**Purpose:** Store before/after photos, customer uploads
**Organization:**
```
/tenants/{tenant_id}/media/
  /jobs/{job_id}/
    /before_001.jpg
    /after_001.jpg
    /video_001.mp4
```
**Access Control:**
- Generate signed URLs for temporary access (24-hour expiration)
- No public access to raw blobs

---

## Technology Stack

### Frontend

| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| **Framework** | React | 18.x | UI components |
| **Meta-Framework** | Next.js | 14.x | SSR, routing, API routes |
| **Styling** | Tailwind CSS | 3.x | Utility-first CSS |
| **State Management** | React Query + Zustand | 5.x / 4.x | Server state + client state |
| **Forms** | React Hook Form | 7.x | Form validation |
| **Charts** | Recharts | 2.x | Analytics dashboards |
| **Calendar** | FullCalendar | 6.x | Booking calendar UI |
| **HTTP Client** | Axios | 1.x | API requests |

---

### Backend

| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| **Runtime** | Node.js | 20 LTS | JavaScript runtime |
| **Framework** | Express.js | 4.x | API framework |
| **Database ORM** | Prisma | 5.x | Type-safe database access |
| **Authentication** | Passport.js + JWT | 0.6.x / 9.x | Auth strategy |
| **Validation** | Zod | 3.x | Schema validation |
| **Email** | SendGrid SDK | 7.x | Transactional emails |
| **File Upload** | Multer | 1.x | File handling |
| **Cron Jobs** | node-cron | 3.x | Scheduled tasks (calendar sync) |

---

### Database

| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| **RDBMS** | PostgreSQL | 16.x | Primary database |
| **Migrations** | Prisma Migrate | 5.x | Schema migrations |
| **Search** | pg_trgm (Postgres ext) | Built-in | Full-text search |
| **Geospatial** | PostGIS (optional) | 3.x | Location-based queries |

---

### Cache & Queue

| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| **Cache** | Redis | 7.x | Session storage, rate limiting |
| **Job Queue** | BullMQ | 5.x | Background jobs (SMS, emails) |

---

### Third-Party Services

| Service | Purpose | Cost (Est.) |
|---------|---------|-------------|
| **Stripe Connect** | Payment processing (deposits, invoices) | 2.9% + $0.30 + platform fee (1.0-1.5%) |
| **Twilio** | SMS messaging (booking confirmations, reminders) | $0.0075/SMS (US) |
| **Mapbox Directions API** | Route optimization, drive time calculation | $0.50/1K requests |
| **Google Calendar API** | Calendar sync (import existing appointments) | Free (up to 1M requests/day) |
| **SendGrid** | Transactional emails (receipts, password resets) | $14.95/mo (50K emails/mo) |

---

### Azure Infrastructure

| Service | Purpose | Cost (Est./mo) |
|---------|---------|----------------|
| **Azure Container Apps** | API hosting (auto-scaling) | $50-200 (based on traffic) |
| **Azure Database for PostgreSQL** | Primary database (2 vCores, 8GB RAM) | $100-150 |
| **Azure Cache for Redis** | Session storage, caching (1GB) | $40-60 |
| **Azure Blob Storage** | Photo/video storage (100GB) | $2-5 |
| **Azure Key Vault** | Secrets management (API keys, DB credentials) | $0.03/10K operations |
| **Azure Front Door** | CDN, WAF, DDoS protection | $50-100 |
| **Azure Application Insights** | Monitoring, logging, alerts | $20-50 |
| **Total** | | **$262-565/mo** (production) |

**Dev/Staging:** ~$50-100/mo (scaled-down resources)

---

## Data Architecture

### Database Schema

#### Core Tables

**tenants**
```sql
CREATE TABLE tenants (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  subdomain VARCHAR(50) UNIQUE NOT NULL,
  business_name VARCHAR(100) NOT NULL,
  email VARCHAR(255) NOT NULL,
  phone VARCHAR(20),
  stripe_customer_id VARCHAR(100),
  stripe_subscription_id VARCHAR(100),
  subscription_status VARCHAR(20) DEFAULT 'active', -- active, past_due, canceled
  subscription_plan VARCHAR(20) DEFAULT 'starter', -- starter, pro, teams
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_tenants_subdomain ON tenants(subdomain);
CREATE INDEX idx_tenants_stripe_customer_id ON tenants(stripe_customer_id);
```

---

**users** (Operator accounts)
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id) ON DELETE CASCADE,
  email VARCHAR(255) NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  role VARCHAR(20) DEFAULT 'owner', -- owner, admin, tech
  name VARCHAR(100),
  phone VARCHAR(20),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(tenant_id, email)
);

CREATE INDEX idx_users_tenant_id ON users(tenant_id);
CREATE INDEX idx_users_email ON users(email);
```

---

**customers**
```sql
CREATE TABLE customers (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id) ON DELETE CASCADE,
  name VARCHAR(100) NOT NULL,
  phone VARCHAR(20) NOT NULL,
  email VARCHAR(255),
  address TEXT,
  notes TEXT,
  total_spent DECIMAL(10, 2) DEFAULT 0,
  last_booking_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(tenant_id, phone)
);

CREATE INDEX idx_customers_tenant_id ON customers(tenant_id);
CREATE INDEX idx_customers_phone ON customers(tenant_id, phone);
CREATE INDEX idx_customers_email ON customers(tenant_id, email);
```

---

**vehicles**
```sql
CREATE TABLE vehicles (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id) ON DELETE CASCADE,
  customer_id UUID REFERENCES customers(id) ON DELETE CASCADE,
  year INT,
  make VARCHAR(50),
  model VARCHAR(50),
  color VARCHAR(30),
  vin VARCHAR(17),
  license_plate VARCHAR(20),
  notes TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_vehicles_tenant_id ON vehicles(tenant_id);
CREATE INDEX idx_vehicles_customer_id ON vehicles(customer_id);
```

---

**service_packages** (Pre-configured services)
```sql
CREATE TABLE service_packages (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id) ON DELETE CASCADE,
  name VARCHAR(100) NOT NULL, -- "Basic Detail", "Full Detail", "Premium"
  description TEXT,
  price DECIMAL(10, 2) NOT NULL,
  duration_minutes INT NOT NULL, -- Used for calendar blocking
  active BOOLEAN DEFAULT true,
  display_order INT DEFAULT 0,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_service_packages_tenant_id ON service_packages(tenant_id);
```

---

**bookings** (Scheduled jobs)
```sql
CREATE TABLE bookings (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id) ON DELETE CASCADE,
  customer_id UUID REFERENCES customers(id),
  vehicle_id UUID REFERENCES vehicles(id),
  service_package_id UUID REFERENCES service_packages(id),
  status VARCHAR(20) DEFAULT 'pending', -- pending, confirmed, in_progress, completed, canceled, no_show
  start_time TIMESTAMP NOT NULL,
  end_time TIMESTAMP NOT NULL,
  address TEXT NOT NULL,
  latitude DECIMAL(10, 8),
  longitude DECIMAL(11, 8),
  total_amount DECIMAL(10, 2) NOT NULL,
  deposit_amount DECIMAL(10, 2) DEFAULT 0,
  notes TEXT,
  source VARCHAR(20) DEFAULT 'platform', -- platform, google_calendar, manual
  technician_id UUID REFERENCES users(id),
  completed_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_bookings_tenant_id ON bookings(tenant_id);
CREATE INDEX idx_bookings_customer_id ON bookings(customer_id);
CREATE INDEX idx_bookings_start_time ON bookings(tenant_id, start_time);
CREATE INDEX idx_bookings_status ON bookings(tenant_id, status);
```

---

**quotes**
```sql
CREATE TABLE quotes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id) ON DELETE CASCADE,
  customer_id UUID REFERENCES customers(id),
  vehicle_id UUID REFERENCES vehicles(id),
  services JSONB NOT NULL, -- [{"name": "Basic Detail", "price": 80}, {"name": "Headlight Restore", "price": 40}]
  total_amount DECIMAL(10, 2) NOT NULL,
  status VARCHAR(20) DEFAULT 'sent', -- sent, viewed, accepted, declined, expired
  expires_at TIMESTAMP,
  accepted_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_quotes_tenant_id ON quotes(tenant_id);
CREATE INDEX idx_quotes_status ON quotes(tenant_id, status);
```

---

**payments**
```sql
CREATE TABLE payments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id) ON DELETE CASCADE,
  booking_id UUID REFERENCES bookings(id),
  stripe_payment_intent_id VARCHAR(100),
  amount DECIMAL(10, 2) NOT NULL,
  payment_method VARCHAR(20) DEFAULT 'card', -- card, cash, check
  status VARCHAR(20) DEFAULT 'pending', -- pending, succeeded, failed, refunded
  refunded_amount DECIMAL(10, 2) DEFAULT 0,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_payments_tenant_id ON payments(tenant_id);
CREATE INDEX idx_payments_booking_id ON payments(booking_id);
CREATE INDEX idx_payments_stripe_id ON payments(stripe_payment_intent_id);
```

---

**messages** (SMS history)
```sql
CREATE TABLE messages (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id) ON DELETE CASCADE,
  customer_id UUID REFERENCES customers(id),
  booking_id UUID REFERENCES bookings(id),
  direction VARCHAR(10) NOT NULL, -- outbound, inbound
  from_phone VARCHAR(20),
  to_phone VARCHAR(20),
  message_body TEXT NOT NULL,
  twilio_message_sid VARCHAR(100),
  status VARCHAR(20) DEFAULT 'sent', -- queued, sent, delivered, failed
  sent_at TIMESTAMP DEFAULT NOW(),
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_messages_tenant_id ON messages(tenant_id);
CREATE INDEX idx_messages_customer_id ON messages(customer_id);
CREATE INDEX idx_messages_booking_id ON messages(booking_id);
```

---

**media** (Photos/videos)
```sql
CREATE TABLE media (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id) ON DELETE CASCADE,
  booking_id UUID REFERENCES bookings(id),
  file_name VARCHAR(255) NOT NULL,
  file_type VARCHAR(50) NOT NULL, -- image/jpeg, video/mp4
  file_size_kb INT NOT NULL,
  blob_url TEXT NOT NULL, -- Azure Blob Storage URL
  category VARCHAR(20) DEFAULT 'before', -- before, after, progress
  uploaded_by UUID REFERENCES users(id),
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_media_tenant_id ON media(tenant_id);
CREATE INDEX idx_media_booking_id ON media(booking_id);
```

---

### Row-Level Security (RLS)

All tables except `tenants` have RLS policies to enforce multi-tenant isolation.

**Example RLS Policy for `bookings` table:**
```sql
ALTER TABLE bookings ENABLE ROW LEVEL SECURITY;

-- Policy: Users can only access their own tenant's bookings
CREATE POLICY tenant_isolation_policy ON bookings
  FOR ALL
  USING (tenant_id = current_setting('app.current_tenant_id')::UUID);
```

**Application sets tenant context:**
```javascript
// Middleware injects tenant_id into database session
app.use(async (req, res, next) => {
  const tenantId = req.user.tenant_id; // From JWT
  await prisma.$executeRaw`SET app.current_tenant_id = ${tenantId}`;
  next();
});
```

---

## Multi-Tenant Architecture

### Tenant Isolation Strategy

**Model:** Shared database, shared schema (all tenants in one PostgreSQL instance)

**Benefits:**
- Cost-effective (single database)
- Easy to manage (one schema, one codebase)
- Fast queries (indexes shared across tenants)

**Trade-offs:**
- Requires careful query filtering (all queries must include `tenant_id`)
- Risk of data leakage if RLS not enforced

### Subdomain Routing

Each tenant gets a unique subdomain for their booking page:

```
mikesdetailing.autoservices.app  →  Tenant ID: 123
joeautospa.autoservices.app      →  Tenant ID: 456
```

**Implementation (Next.js Middleware):**
```javascript
// middleware.ts
export function middleware(request) {
  const hostname = request.headers.get('host');
  const subdomain = hostname.split('.')[0];

  // Lookup tenant by subdomain
  const tenant = await prisma.tenant.findUnique({
    where: { subdomain }
  });

  if (!tenant) {
    return new Response('Tenant not found', { status: 404 });
  }

  // Inject tenant ID into request headers
  request.headers.set('x-tenant-id', tenant.id);
  return NextResponse.next();
}
```

### Data Isolation

**Database-level:**
- All queries filtered by `tenant_id` (enforced via RLS)
- Backup strategy: Full database backup (all tenants), restore by tenant if needed

**Blob Storage:**
- Files organized by `tenant_id`: `/tenants/{tenant_id}/media/`
- Signed URLs prevent cross-tenant access

**Cache (Redis):**
- All cache keys prefixed with `tenant:{tenant_id}:`
- Example: `tenant:123:session:abc` vs. `tenant:456:session:xyz`

### Tenant Limits & Quotas

| Resource | Starter Plan | Pro Plan | Teams Plan |
|----------|--------------|----------|------------|
| **Technicians** | 1 | 5 | 10 |
| **Jobs/Month** | 100 | Unlimited | Unlimited |
| **Customers** | 500 | 5,000 | 10,000 |
| **Media Storage** | 1GB | 10GB | 50GB |
| **SMS Messages** | 100/mo | 500/mo | 2,000/mo |
| **API Rate Limit** | 1K req/hour | 10K req/hour | 50K req/hour |

**Enforcement:**
- Check quota before allowing operation (e.g., create booking, upload photo)
- Display usage on dashboard (e.g., "47/100 jobs this month")
- Soft limit warnings at 80%, hard limit at 100%

---

## Third-Party Integrations

### 1. Stripe Connect (Payments)

**Purpose:** Process deposits, invoices, and subscriptions on behalf of tenants

**Integration Type:** Stripe Connect (Standard Connected Accounts)

**Flow:**
```
1. Tenant signs up → Create Stripe Connected Account
2. Customer books job → Create Stripe Checkout Session (50% deposit)
3. Payment succeeds → Webhook: `checkout.session.completed` → Confirm booking
4. Job completed → Charge remaining 50% to card-on-file (Payment Intent)
5. Platform collects 1.0-1.5% platform fee on top of Stripe fees
```

**Key Endpoints:**
- `POST /api/payments/create-checkout-session` → Create Stripe Checkout
- `POST /api/webhooks/stripe` → Handle Stripe webhooks
- `POST /api/payments/refund` → Refund deposit (Stripe Refund API)

**Security:**
- Stripe API keys stored in Azure Key Vault
- Webhook signature validation (verify `stripe-signature` header)

---

### 2. Twilio (SMS Messaging)

**Purpose:** Send booking confirmations, reminders, and payment notifications

**Integration Type:** Twilio Programmable Messaging API

**Message Types:**
- **Booking confirmation:** Sent immediately after deposit paid
- **Day-before reminder:** Sent 24 hours before appointment
- **On-the-way notification:** Sent when tech starts driving to job
- **Payment reminder:** Sent for unpaid invoices (7 days, 14 days)

**Key Endpoints:**
- `POST /api/messages/send` → Send SMS via Twilio
- `POST /api/webhooks/twilio` → Receive incoming SMS (2-way messaging)

**Cost Management:**
- Charge $0.05/SMS after 100/500/2000 messages (based on plan)
- Option to disable SMS and use email-only

---

### 3. Mapbox Directions API (Route Optimization)

**Purpose:** Calculate optimal route order to minimize drive time

**Integration Type:** Mapbox Directions API (Optimization endpoint)

**Flow:**
```
1. Operator views daily schedule with 6 jobs
2. System sends job addresses to Mapbox Optimization API
3. Mapbox returns optimal visit order + drive times
4. System suggests: "Save 45 min by reordering Job B and Job D"
5. Operator approves → Route locked in → ETAs sent to customers
```

**Key Endpoints:**
- `POST /api/routes/optimize` → Optimize daily route
- `GET /api/routes/:date` → View optimized route for specific date

**Fallback:**
- If Mapbox API fails, fall back to simple distance-based sorting (nearest-neighbor)

---

### 4. Google Calendar API (Calendar Sync)

**Purpose:** Import existing appointments to prevent double-bookings

**Integration Type:** Google Calendar API (OAuth 2.0)

**Flow:**
```
1. Operator connects Google Calendar (OAuth flow)
2. System imports events from next 30 days
3. Imported events block time slots on booking calendar
4. Cron job syncs every 15 minutes (poll for new events)
5. Operator can disconnect integration anytime
```

**Key Endpoints:**
- `POST /api/integrations/google-calendar/connect` → Initiate OAuth
- `POST /api/integrations/google-calendar/sync` → Manual sync
- `DELETE /api/integrations/google-calendar/disconnect` → Revoke access

**Storage:**
- OAuth refresh token encrypted and stored in `tenants` table
- Imported events stored in `bookings` table with `source = 'google_calendar'`

---

## Security & Compliance

### Authentication & Authorization

**Authentication:**
- Email/password login with bcrypt password hashing (cost factor: 12)
- JWT tokens issued upon login (7-day expiration)
- Refresh tokens stored in httpOnly cookies (prevent XSS)

**Authorization:**
- Role-based access control (RBAC): `owner`, `admin`, `tech`
- Middleware checks JWT and role before allowing protected endpoints

**Example:**
```javascript
// Require authentication
app.use('/api', requireAuth);

// Require owner role
app.use('/api/settings', requireRole('owner'));

// Technicians can only view their own assigned jobs
app.get('/api/bookings', async (req, res) => {
  const { user } = req;
  const filter = user.role === 'tech' ? { technician_id: user.id } : {};
  const bookings = await prisma.booking.findMany({ where: filter });
  res.json(bookings);
});
```

---

### Data Encryption

**In Transit:**
- All communication over HTTPS (TLS 1.3)
- API enforces HTTPS-only (redirect HTTP → HTTPS)

**At Rest:**
- PostgreSQL: Transparent Data Encryption (TDE) enabled
- Blob Storage: Server-side encryption (SSE) with Microsoft-managed keys
- Secrets: Stored in Azure Key Vault (encrypted)

---

### PCI DSS Compliance

**Strategy:** Use Stripe to avoid handling raw card data

**Compliance Requirements:**
- ✅ Never store raw card numbers (Stripe stores cards)
- ✅ Use Stripe.js for card input (card data never touches our servers)
- ✅ Only store Stripe token IDs (e.g., `pm_abc123`)
- ✅ Webhook signature validation (prevent spoofed webhooks)

**Certification:** Not required (Stripe is PCI Level 1 certified; we rely on their compliance)

---

### GDPR & CCPA Compliance

**User Rights:**
1. **Right to Access:** Provide customer data export (CSV download)
2. **Right to Deletion:** Delete customer account and all associated data (cascade delete)
3. **Right to Portability:** Export data in machine-readable format (JSON)

**Implementation:**
- `GET /api/customers/:id/export` → Export customer data (JSON)
- `DELETE /api/customers/:id` → Soft delete customer (30-day grace period)
- `POST /api/customers/:id/anonymize` → Anonymize customer data (GDPR "right to be forgotten")

**Data Retention:**
- Customer data retained for 7 years (tax compliance)
- Deleted accounts soft-deleted (30 days), then hard-deleted
- Media files deleted immediately upon account deletion

---

### Rate Limiting

**Purpose:** Prevent API abuse and DDoS attacks

**Limits:**
- **Public endpoints** (booking pages): 100 requests/minute per IP
- **Authenticated endpoints** (API): 1,000 requests/hour per tenant (Starter), 10K/hour (Pro)
- **Webhook endpoints:** Unlimited (but signature-validated)

**Implementation:**
- Use Redis for rate limit counters
- Middleware checks rate limit before processing request
- Return `429 Too Many Requests` if limit exceeded

```javascript
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  store: new RedisStore({ client: redisClient }),
  windowMs: 60 * 60 * 1000, // 1 hour
  max: (req) => req.user.subscription_plan === 'pro' ? 10000 : 1000,
  message: 'Rate limit exceeded'
});

app.use('/api', limiter);
```

---

## Scalability & Performance

### Horizontal Scaling

**Azure Container Apps:**
- Auto-scale based on CPU and memory usage
- Scale from 1 to 10 instances (production), 1 to 3 (dev/staging)
- Load balancing handled automatically

**Configuration:**
```yaml
resources:
  cpu: 1.0
  memory: 2Gi
scale:
  minReplicas: 2
  maxReplicas: 10
  rules:
    - name: cpu-scaling
      type: cpu
      metadata:
        type: Utilization
        value: "70"
```

---

### Database Performance

**PostgreSQL Optimization:**
- **Indexes:** All foreign keys, `tenant_id`, `created_at`, `status` columns indexed
- **Connection pooling:** Prisma connection pool (max 20 connections per instance)
- **Read replicas:** Optional (post-PMF) for reporting queries
- **Query optimization:** Use `EXPLAIN ANALYZE` to identify slow queries

**Example Slow Query Fix:**
```sql
-- Slow query (missing index)
SELECT * FROM bookings WHERE tenant_id = '123' AND start_time > NOW();

-- Add index
CREATE INDEX idx_bookings_start_time ON bookings(tenant_id, start_time);

-- Fast query (uses index)
-- Execution time: 5ms → 1ms
```

---

### Caching Strategy

**Redis Caching:**
1. **Session storage:** JWT tokens cached for fast lookup
2. **Service packages:** Cache tenant-specific packages (rarely change)
3. **Tenant settings:** Cache working hours, buffer times, no-show fees

**Cache Invalidation:**
- **TTL:** 1 hour for most keys
- **Manual invalidation:** When settings changed, clear relevant cache keys

```javascript
// Cache service packages
const cacheKey = `tenant:${tenantId}:service_packages`;
let packages = await redis.get(cacheKey);

if (!packages) {
  packages = await prisma.servicePackage.findMany({ where: { tenant_id: tenantId } });
  await redis.set(cacheKey, JSON.stringify(packages), 'EX', 3600); // 1 hour TTL
}
```

---

### CDN & Static Assets

**Azure Front Door:**
- Cache static assets (CSS, JS, images) at edge locations
- Reduce latency for global users
- DDoS protection and WAF (Web Application Firewall)

**Configuration:**
- Cache booking pages for 5 minutes (balance freshness vs. performance)
- Cache API responses: No (dynamic data)
- Cache media files (photos): 24 hours

---

## DevOps & CI/CD

### CI/CD Pipeline (GitHub Actions)

**Workflow:**
```yaml
# .github/workflows/deploy-staging.yml
name: Deploy to Staging

on:
  push:
    branches: [develop]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Build Docker Image
        run: docker build -t app-vrd-202513-stg-eus2-01 .

      - name: Push to Azure Container Registry
        run: |
          az acr login --name acrvrd202513
          docker push acrvrd202513.azurecr.io/app-vrd-202513-stg-eus2-01

      - name: Deploy to Azure Container Apps
        run: |
          az containerapp update \
            --name app-vrd-202513-stg-eus2-01 \
            --resource-group rg-vrd-202513-stg-eus2-app \
            --image acrvrd202513.azurecr.io/app-vrd-202513-stg-eus2-01:latest

      - name: Run Database Migrations
        run: npx prisma migrate deploy
```

**Environments:**
- **develop** branch → Auto-deploy to **Staging**
- **main** branch → Manual approval → Deploy to **Production**
- **feature/** branches → No auto-deploy (PR preview optional)

---

### Infrastructure as Code (Bicep)

**Deployment:**
```bash
# Deploy complete infrastructure
az deployment sub create \
  --location eastus2 \
  --template-file infrastructure/bicep/main.bicep \
  --parameters org=vrd proj=202513 env=prd primaryRegion=eus2
```

**What Gets Deployed:**
- Container Apps (API service)
- PostgreSQL database
- Redis cache
- Blob Storage
- Key Vault
- Application Insights

**See:** `infrastructure/bicep/` for templates

---

## Monitoring & Observability

### Application Insights

**Metrics:**
- Request rate (requests/sec)
- Error rate (% failed requests)
- Response time (p50, p95, p99)
- Dependency calls (Stripe, Twilio, Mapbox)

**Alerts:**
- Error rate > 5% for 5 minutes → Alert ops team
- Response time p95 > 2 seconds → Alert ops team
- Database CPU > 80% → Alert ops team

---

### Logging

**Structured Logging:**
```javascript
const logger = require('winston');

logger.info('Booking created', {
  tenant_id: tenantId,
  booking_id: bookingId,
  customer_phone: customerPhone,
  total_amount: totalAmount
});
```

**Log Retention:**
- Application logs: 30 days (Application Insights)
- Database query logs: 7 days
- Webhook logs: 90 days (compliance)

---

### Uptime Monitoring

**Azure Monitor:**
- Ping `/health` endpoint every 5 minutes
- Alert if 3 consecutive failures (downtime > 15 min)

**Health Check Endpoint:**
```javascript
app.get('/health', async (req, res) => {
  const checks = {
    database: await checkDatabase(),
    redis: await checkRedis(),
    stripe: await checkStripe()
  };

  const healthy = Object.values(checks).every(v => v === true);
  res.status(healthy ? 200 : 503).json(checks);
});
```

---

## Appendix

### Related Documents

- **Multi-Tenant Architecture Guide:** `technical/multi-tenant-architecture.md`
- **Azure Deployment Guide:** `technical/infrastructure/AZURE-DEPLOYMENT-GUIDE.md`
- **Azure Security Baseline:** `technical/azure-security-zero-to-prod-v2.md`
- **API Specification:** `technical/api/api-spec.md` (to be created)
- **Database Schema:** `technical/architecture/database-schema.sql` (to be created)

---

**End of Architecture Document**
