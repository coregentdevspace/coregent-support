# SparkLine Electrical – Product Requirements Document

**Version:** 2.0
**Last Updated:** 2025-12-29
**Status:** Production Release

---

## 1. Project Overview

SparkLine Electrical is a comprehensive digital platform for a local electrical services business operating in Canberra and the Australian Capital Territory (ACT). The platform includes:

- A **public website** for potential customers to:
  - Learn about electrical services (11 service categories)
  - View completed work gallery with project details
  - Read and submit customer reviews
  - Check service areas with response times
  - Submit quote requests and general enquiries
  - Access FAQs organized by category
- An **admin portal** for business staff to:
  - View dashboard with statistics and recent activity
  - Manage quote requests and contact messages
  - Moderate customer reviews (approve/reject/spam/feature)
  - Send marketing emails to consented customers with template management
  - Manage admin users with role-based permissions

The site is designed as a **reusable template** for other local service businesses (e.g., plumbing, HVAC, landscaping), with most functionality being generic to enquiry-driven local services.

**Demo Mode:** The current deployment includes a demo banner indicating this is a showcase version with placeholder contact details (02 0000 0000).

---

## 2. Technology Stack

| Category | Technology |
|----------|------------|
| Framework | Next.js 16 (App Router with Turbopack) |
| Language | TypeScript |
| UI Library | React 19 |
| Styling | Tailwind CSS 4 |
| Components | shadcn/ui (59 components), Radix UI primitives |
| Database | Supabase (PostgreSQL) |
| Authentication | Supabase Auth (email/password) |
| Email Service | Resend API |
| Email Templates | React Email |
| Forms | React Hook Form + Zod validation |
| Icons | Lucide React |
| Charts | Recharts |
| Carousel | Embla Carousel |
| Notifications | Sonner (toast) |
| Theme | next-themes (dark/light mode) |

---

## 3. Objectives

- **Generate qualified leads** through service-specific quote request forms
- **Establish trust and credibility** via customer reviews, team profiles, company history, and visual evidence of work
- **Present strong social proof** using reviews, testimonials, and gallery content
- **Provide 24/7 access** to service information and emergency contact details
- **Streamline operations** with centralized management of customer enquiries and quote requests
- **Build a customer database** with consent-based marketing capabilities
- **Showcase expertise** using:
  - Coverage of specific service areas and suburbs with response times
  - Team credentials and years of experience
  - Completed project gallery with detailed case studies
- **Serve as a reusable template** for other local service businesses beyond electrical

---

## 4. User Roles

### 4.1 Public Visitor / Customer

- Browse all public pages without logging in
- View detailed service information (11 categories) and service areas
- Read approved customer reviews with ratings and statistics
- View gallery with project details, challenges, and solutions
- Access FAQs organized by category
- Submit:
  - Quote request forms (with service type, urgency, project description)
  - General contact messages
  - Customer reviews/testimonials (with spam protection)

### 4.2 Admin User

- Log in to secure admin portal via email/password
- Access admin dashboard with statistics overview
- View and manage:
  - Quote requests (with customer details, service type, urgency, location)
  - Contact messages
  - Customer reviews (with full moderation workflow)
- Change own password

### 4.3 Admin User with Marketing Permissions

- All capabilities of standard admin user, plus:
  - Compose and send marketing emails to customers with marketing consent
  - Manage email templates (system + custom templates)
  - Preview emails before sending
  - Send test emails to specified addresses
  - View email campaign history with recipient counts

### 4.4 Admin User with User Management Permissions (Super Admin)

- All capabilities of marketing admin, plus:
  - View list of admin users with roles and status
  - Add new admin users
  - Edit admin user profiles
  - Delete/deactivate admin accounts

---

## 5. Public Website Features

### 5.1 Home Page (`/`)

**Purpose:** Main landing and conversion page introducing SparkLine Electrical with clear pathways to request quotes or call.

**Implemented Sections:**

- **Demo Banner**
  - Cyan notification bar indicating demo/showcase status
  - Displayed at top of all pages

- **Hero Section**
  - Strong headline and subheading for local electrical needs
  - Emergency contact number (24/7)
  - Primary CTA: "Request a Quote"
  - Secondary CTA: "Call Now" (clickable tel: link)

- **Services Overview**
  - Service cards with icons linking to detail pages
  - Covers all 11 service categories

- **Trust & Social Proof Section**
  - Certifications, licenses, years in business
  - Statistics display (jobs completed, experience, customers, rating)

- **Featured Testimonials**
  - Carousel displaying featured or top-rated reviews
  - Shows reviewer name, suburb, rating, and review text
  - Powered by `TestimonialsCarouselClient` component

- **Closing CTA**
  - Final prompt to request quote or call

---

### 5.2 About Page (`/about`)

**Purpose:** Company story, values, team overview, and credibility building.

**Implemented Sections:**

- **Company Story**
  - Narrative about origins, mission, and commitment to quality

- **Timeline Journey**
  - Visual timeline showing milestones from founding to present

- **Team Showcase**
  - Team member carousel with photos, names, and roles
  - Data sourced from `team-members.ts`
  - Includes team metrics (technicians, combined experience)

- **Qualifications & Certifications**
  - List of licenses, memberships, and insurance

- **Community & Culture**
  - Local community involvement and workplace values

- **CTA Section**
  - Links to Request a Quote and Contact pages

---

### 5.3 Services Overview Page (`/services`)

**Purpose:** Comprehensive overview of all 11 service categories.

**Implemented Service Categories:**

1. 24/7 Emergency Electrical
2. Lighting & Ceiling Fans
3. Switchboard Upgrades
4. Power Points & Wiring
5. Safety Switches & Smoke Alarms
6. EV Charger Installation
7. Commercial Electrical
8. Data & Communications
9. Air Conditioning Electrical
10. Solar & Battery Systems
11. General Electrical

**Key Features:**

- Hero section with service availability messaging
- Service cards grid with icons and descriptions
- Each card links to detailed service page
- Service area reminder
- CTA to request quote

---

### 5.4 Service Detail Pages (`/services/[id]`)

**Purpose:** In-depth, service-specific information for conversions.

**Implemented Content:**

- **Hero Image** - Large relevant image/illustration
- **Detailed Description** - What the service covers
- **Benefits / Why Choose Us** - Licensed electricians, transparent pricing, fast response
- **Common Issues Handled** - List of typical problems
- **What's Included** - Process overview (assessment, quote, repair, clean-up)
- **CTAs** - Call emergency line, Request a Quote

**Dynamic Routing:** Pages generated from service type data with `generateStaticParams`.

---

### 5.5 Service Areas Page (`/areas`)

**Purpose:** Coverage explanation with response time expectations.

**Implemented Regions:**

1. Belconnen
2. Canberra Central
3. Gungahlin
4. Tuggeranong
5. Woden Valley
6. Weston Creek
7. Molonglo Valley
8. Queanbeyan & Surrounds

**Features:**

- Coverage overview description
- Region cards with suburb lists (15+ suburbs each)
- Response time indicators (e.g., "< 30 mins" for central areas)
- Full suburb listings under each region
- CTA for quote requests

---

### 5.6 Reviews Page (`/reviews`)

**Purpose:** Build trust via customer feedback and allow new submissions.

**Implemented Features:**

- **Hero Section** - Review process explanation
- **Review Statistics** - Average rating, total approved reviews (via `getReviewStats()`)
- **Reviews List** - Cards showing:
  - Customer first name and suburb
  - Star rating (1-5)
  - Optional title
  - Review text
  - Service type and date (if provided)
- **Review Submission Form** - Full form with validation and spam protection

**Business Rules:**

- Only reviews with status "approved" appear publicly
- Reviews moderated by admin before publishing
- Featured reviews promoted on home page
- `ReviewSubmissionForm` includes honeypot field for spam detection
- IP address and user agent recorded for spam analysis

---

### 5.7 Gallery Page (`/gallery`)

**Purpose:** Visual proof of quality and range of completed work.

**Implemented Features:**

- **Hero Section** - Portfolio introduction
- **Gallery Grid** - Project images with titles and categories
- **Business Statistics:**
  - 1000+ jobs completed
  - 10+ years in business
  - 500+ satisfied customers
  - 4.9/5 average rating

**Data Source:** `gallery-items.ts` with project entries including:
- Title, description, category
- Location, duration
- Detailed project story
- Highlights, challenges, solutions

---

### 5.8 Gallery Detail Pages (`/gallery/[id]`)

**Purpose:** Detailed case study for individual projects.

**Implemented Content:**

- Project hero image
- Full project description and story
- Key highlights list
- Challenges faced
- Solutions implemented
- Location and duration
- Related projects navigation
- CTA to request quote

---

### 5.9 FAQs Page (`/faqs`)

**Purpose:** Answer common questions to reduce support burden.

**Implemented Categories:**

1. Emergency Services
2. Services & Pricing
3. Licensing & Qualifications
4. Scheduling & Booking

**Features:**

- Accordion-style interface
- Click to expand/collapse answers
- Inline CTAs within answers
- CTA section at bottom

---

### 5.10 Request a Quote Page (`/quote`)

**Purpose:** Capture detailed information for accurate quoting.

**Implemented Form Fields:**

**Contact Information:**
- First Name (required)
- Last Name (optional)
- Email Address (required, validated)
- Phone Number (optional)
- Preferred Name (optional)
- Street Address (required)
- Suburb (required)
- State (required, dropdown)
- Postcode (required)

**Project Details:**
- Type of Service (required, dropdown - 11 options)
- Urgency (required, dropdown - 5 levels)
- Project Description (required, free-text)
- Preferred Contact Time (optional)
- Marketing Consent (optional, IconCheckbox)

**Urgency Levels:**
1. ASAP (Emergency)
2. Within 24 hours
3. This week
4. Next week
5. Flexible

**Form Behaviour:**
- Required field validation with inline errors
- Email format validation
- Loading indicator during submission
- Success screen with confirmation and quote ID
- Emergency contact reminder

**After Submission:**
- Quote confirmation email to customer
- Notification email to admin/business
- Data stored: user_profile, address, quote_request tables

---

### 5.11 Contact Page (`/contact`)

**Purpose:** Multiple channels for general enquiries.

**Implemented Sections:**

- **Hero/Intro** - Invitation to get in touch
- **Contact Info Cards:**
  - Emergency phone (24/7)
  - Email address
  - Service area description
  - Business hours
- **Contact Form:**
  - First Name (required)
  - Last Name (optional)
  - Email Address (required, validated)
  - Phone Number (optional)
  - Message (required, free-text)
  - Marketing Consent (optional, IconCheckbox)
- **Emergency CTA** - Reminder to call for urgent issues

**After Submission:**
- Confirmation email to customer
- Notification email to admin
- Message stored in database

---

### 5.12 Authentication Pages (`/auth/*`)

**Purpose:** Secure access to admin portal.

**Implemented Pages:**

| Route | Purpose |
|-------|---------|
| `/auth/login` | Email + password login form |
| `/auth/sign-up` | New admin registration |
| `/auth/sign-up-success` | Post-signup confirmation |
| `/auth/forgot-password` | Password reset request |
| `/auth/update-password` | Set new password after reset |
| `/auth/confirm` | Email confirmation callback handler |
| `/auth/error` | Authentication error display |

**Business Rules:**
- Admin authentication required for all admin features
- Password resets require email verification
- Session managed via Supabase Auth with cookie-based strategy

---

## 6. Navigation & Layout

### 6.1 Header Component

**Features:**
- Logo linking to home
- Main navigation links (desktop): Services, About, Service Areas, Gallery, Reviews, FAQs, Contact
- Phone number with "Demo only" indicator
- "Request Quote" CTA button (desktop)
- **Mobile Navigation** (`MobileNav` component):
  - Hamburger menu icon (visible on mobile)
  - Sheet/drawer sliding from right
  - All navigation links with active state highlighting
  - Request Quote button
  - Phone number display
  - Auto-closes on link click
- Sticky header on scroll

### 6.2 Footer Component

**Features:**
- Business contact details (phone, email)
- Quick links to main pages
- Business hours
- Social media links (placeholder)
- Copyright and legal links

---

## 7. Admin Panel Features

### 7.1 Admin Layout (`/admin`)

**Navigation Sidebar:**
- Dashboard
- Quote Requests
- Messages
- Reviews
- Marketing (permission-based)
- Users (permission-based)

**Header:**
- Current section title
- User account menu
- Logout functionality

---

### 7.2 Dashboard (`/admin/dashboard`)

**Purpose:** Quick snapshot of activity and entry points to admin functions.

**Implemented Metrics:**
- Total quote requests (all time)
- Total contact messages
- Total reviews (all statuses)
- Total user profiles

**Recent Activity:**
- Recent quote requests (latest items)
- Recent messages (latest items)
- Click to navigate to full lists

---

### 7.3 Quote Requests Management (`/admin/quotes`)

**Purpose:** Review and act on all quote requests.

**Display per Quote:**
- Customer name with avatar/initials
- Email (clickable mailto link)
- Phone (clickable tel link)
- Full address (street, suburb, state, postcode)
- Preferred contact time
- Service type (badge)
- Urgency (colored badge - red for emergency)
- Project description (`project_desc` field)
- Submission date/time

**Features:**
- Reverse chronological order
- Empty state messaging
- Click-to-contact functionality

---

### 7.4 Messages Management (`/admin/messages`)

**Purpose:** Central place for general enquiries and feedback.

**Display per Message:**
- Customer name with avatar/initials
- Email and phone (if provided)
- Full message text
- Submission date/time

**Features:**
- Newest first ordering
- Click-to-respond functionality
- Empty state messaging

---

### 7.5 Reviews Management (`/admin/reviews`)

**Purpose:** Curate customer reviews and maintain quality.

**Filter Tabs:**
- All
- Pending
- Approved
- Rejected
- Spam

**Review Card Display:**
- Customer info: name, suburb, email, phone
- Review content: rating (stars), title, body
- Service type and date
- Metadata: submission date, status
- Internal: IP address, user agent, admin notes
- Featured flag indicator

**Actions:**
- Approve review
- Reject review
- Mark as spam
- Toggle featured status
- Add/edit admin notes
- Delete review (soft delete)

**Business Rules:**
- Only approved reviews appear publicly
- Featured reviews get priority on home page
- Admin notes and technical metadata never shown publicly
- Published date tracked separately from submission date

---

### 7.6 Marketing Emails (`/admin/marketing`)

**Purpose:** Send promotional campaigns to consented users.

**Composer Features:**
- Subject line input (required)
- Rich text editor (TipTap) for HTML content:
  - Headings, paragraphs, lists
  - Links, bold, italic formatting
  - Placeholder support for variables
- Automatic plain-text version generation

**Template Management:**
- Load existing templates (system + custom)
- Save current content as template
- Edit template name and content
- Delete custom templates
- Templates stored per customer

**Personalization Variables:**
- `{firstName}` - Customer first name
- `{lastName}` - Customer last name
- `{preferredName}` - Preferred name
- `{email}` - Customer email
- Variable documentation displayed in UI

**Recipient Selection:**
- List of users with `marketing_consent = true`
- Select all / deselect all
- Individual checkboxes
- Selected recipient count display

**Testing & Sending:**
- Preview email as recipient sees it (`EmailPreviewDialog`)
- Send test email to specified address (`TestEmailDialog`)
- Send campaign with confirmation dialog (`SendConfirmationDialog`)

**Email History:**
- Subject, send date/time
- Sender (admin user)
- Recipient count
- Content snapshot stored
- Audit trail for compliance

---

### 7.7 Users Management (`/admin/users`)

**Purpose:** Manage admin portal access.

**User List Display:**
- Name with avatar/initials
- Email address
- Role/permissions
- Status (Active/Inactive)
- Join date
- Last login (if available)

**Actions:**
- Add new admin user (`AddUserDialog`)
- Edit user profile
- Change password (`ChangePasswordDialog`)
- Delete/deactivate user

**Business Rules:**
- Only super admins can access user management
- Email must be unique per admin user
- Role determines feature access

---

## 8. Email System

### 8.1 Transactional Emails (Customers)

**Quote Request Confirmation** (`quote-confirmation.tsx`):
- Trigger: Quote form submission
- Content: Customer name, quote ID, service type, urgency, address, response timeframe, emergency contact

**Contact Message Confirmation** (`message-confirmation.tsx`):
- Trigger: Contact form submission
- Content: Customer name, acknowledgement, response timeframe, emergency contact reminder

### 8.2 Transactional Emails (Admin)

**New Quote Notification** (`quote-admin-notification.tsx`):
- Trigger: Quote form submission
- Content: All quote details, customer contact info, project description

**New Message Notification** (`message-admin-notification.tsx`):
- Trigger: Contact form submission
- Content: Message text, customer details, marketing consent status

### 8.3 Marketing Emails (`marketing-email.tsx`)

- Triggered manually via admin interface
- Variable substitution per recipient
- HTML and plain-text versions
- Campaign history logging
- Only sent to consented users

### 8.4 Email Configuration

- **Service:** Resend API
- **Templates:** React Email (JSX-based)
- **Config Storage:** `customer` table (notification_email, from_email_address)
- **Async Delivery:** Email sending doesn't block form submission

---

## 9. Database Schema

### 9.1 Core Tables

| Table | Purpose | Key Fields |
|-------|---------|------------|
| `customer` | Business configuration | customer_id, notification_email, from_email_address |
| `user_profile` | Customer profiles | user_id, email, first_name, last_name, phone, marketing_consent |
| `user_login` | Admin authentication | login_id, auth_user_id, email, role, status |
| `address` | User addresses | address_id, user_id, address, suburb, state, postcode |
| `quote_request` | Quote submissions | quote_request_id, user_id, service_type_id, urgency_id, project_desc |
| `message` | Contact messages | message_id, user_id, user_message |
| `review` | Customer reviews | review_id, rating, review_body, status, is_featured |
| `service_type` | Reference data (11 types) | service_type_id, service_name, display_order |
| `urgency` | Reference data (5 levels) | urgency_id, urgency_name, display_order |
| `marketing_email_template` | Email templates | template_id, template_name, subject, body_html |
| `marketing_email_history` | Email audit trail | email_id, subject, recipient_count, sent_at |

### 9.2 Security

- **Row Level Security (RLS)** enabled on all tables
- Anonymous users: insert quotes/messages, read reference data
- Authenticated admins: full CRUD access
- Service role client for admin operations

---

## 10. Forms & Validation

### 10.1 Quote Request Form

**Validation Rules:**
- First name: required
- Email: required, format validation
- Address fields: all required
- Service type: required (dropdown)
- Urgency: required (dropdown)
- Project description: required

**Spam Protection:**
- Client-side validation
- Server-side validation via server actions

### 10.2 Contact Message Form

**Validation Rules:**
- First name: required
- Email: required, format validation
- Message: required

### 10.3 Review Submission Form

**Validation Rules:**
- Rating: required (1-5 stars)
- First name: required (2-80 characters)
- Review body: required (20-2000 characters)
- Consent checkbox: required
- Email: format validation if provided

**Spam Protection:**
- Honeypot field (must remain empty)
- IP address tracking
- User agent recording

---

## 11. Static Data Sources

### 11.1 Gallery Items (`src/data/gallery-items.ts`)

Project entries with:
- id, title, description, category
- image path, location, duration
- Detailed story narrative
- Highlights array
- Challenges and solutions

### 11.2 Team Members (`src/data/team-members.ts`)

Team profile data for About page carousel.

### 11.3 Service Areas

Region and suburb data embedded in Areas page component.

### 11.4 FAQs

Question/answer data embedded in FAQs page component.

---

## 12. API Routes

| Route | Purpose |
|-------|---------|
| `/api/test-env` | Environment variable testing |
| `/auth/confirm` | Email confirmation callback handler |

**Server Actions:**
- `submitQuoteAction()` - Quote form submission
- `submitMessageAction()` - Contact form submission

---

## 13. Deployment

### 13.1 Platform

- **Hosting:** Vercel
- **Database:** Supabase (hosted PostgreSQL)
- **Domain:** sparkline.coregent.com.au

### 13.2 Environment Variables

Required:
- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`
- `SUPABASE_SERVICE_ROLE_KEY`
- `RESEND_API_KEY`

### 13.3 Build Configuration

- Next.js 16 with Turbopack
- Static generation for service and gallery detail pages
- Server-side rendering for dynamic content

---

## 14. Future Enhancements (Not Yet Implemented)

### 14.1 Workflow Improvements

- Quote/message status tracking (New, Contacted, Converted, Archived)
- Assignment to specific staff members
- Export/reporting capabilities

### 14.2 Content Management UI

- Admin UI for services, FAQs, gallery, service areas
- Global settings management (business hours, contact details)

### 14.3 Review Enhancements

- Public business responses to reviews
- Review filtering/sorting for visitors
- Analytics on ratings over time

### 14.4 Marketing Analytics

- Email open rates and click-through tracking
- Unsubscribe metrics
- Campaign performance dashboard

### 14.5 CRM & Job Management

- Converting quotes to jobs
- Scheduling and job notes
- Per-customer history view

### 14.6 Multi-Tenancy

- Single deployment serving multiple businesses
- Separate admin access and branding per tenant

---

## 15. Summary

SparkLine Electrical v2.0 provides a complete, production-ready digital platform for an electrical services business with:

**Customer-Facing Features:**
- 11 service category pages with detailed information
- Quote request and contact forms with email confirmations
- Review submission with moderation workflow
- Project gallery with detailed case studies
- Service area coverage with response times
- Organized FAQs
- Mobile-responsive design with slide-out navigation

**Business-Facing Features:**
- Comprehensive admin dashboard
- Quote and message management
- Full review moderation system (approve/reject/spam/feature)
- Marketing email campaigns with template management
- Admin user management with role-based access
- Email history and audit trail

**Technical Foundation:**
- Next.js 16 with React 19
- Supabase for database and authentication
- Resend for transactional and marketing emails
- 59 shadcn/ui components
- TypeScript throughout
- Tailwind CSS styling

The platform is designed for reuse across other local service businesses with minimal customization required.

---

**End of Document**
