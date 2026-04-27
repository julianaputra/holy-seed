# Holy Seed - Plant Seed E-Commerce - Product Requirements Document (PRD)
**Version:** 01
**Date:** April 27, 2026
**Product Owner:** PT Timedoor Indonesia
**Status:** Draft - Pending Approval

---

## 1. Product Overview

### 1.1 Vision
**Holy Seed** is a simple e-commerce platform that makes it easy for plant lovers to purchase high-quality plant seeds online, featuring a complete product catalog, a smooth ordering process, and trackable shipping.

### 1.2 Target Users
- **Customer (Buyer)** - Plant lovers, hobbyists, beginner farmers, and home gardeners
- **Admin (Shop Manager)** - Manages product catalog, stock, and orders

### 1.3 Key Value Propositions
1. **Complete Catalog**: A wide variety of plant seeds (vegetables, fruits, ornamentals) in one place
2. **Simple Process**: Shop, checkout, and pay in just a few clicks
3. **Clear Information**: Detailed seed info (planting guide, harvest time, water & sunlight needs)
4. **Order Tracking**: Customers can monitor order status in real time
5. **Easy Stock Management**: Admins can manage products and orders quickly

### 1.4 Technology Stack

#### Backend
- **Framework**: Laravel 11 (PHP 8.2+)
- **Authentication**: Laravel Passport (OAuth2 with JWT-based tokens)
- **Database**: MySQL 8.0+
- **API**: RESTful API with JSON response format
- **File Storage**: Laravel Storage (local) for product images

#### Frontend
- **Framework**: Next.js 14+ (App Router) with TypeScript
- **UI Library**: shadcn/ui (Radix UI components built on Tailwind)
- **Styling**: Tailwind CSS 3+
- **HTTP Client**: Axios or Fetch API for backend communication
- **State Management**: React Context or Zustand for cart & auth
- **Form Validation**: React Hook Form + Zod

#### Development & Deployment
- **Version Control**: Git (GitHub/GitLab)
- **API Documentation**: Postman Collection or Swagger
- **Environment**: `.env` for configuration (database, API URL, etc.)

#### Architecture
- **Separation of Concerns**: Laravel backend (API) and Next.js frontend run independently
- **Communication**: Frontend calls the backend REST API using a Bearer Token (Passport)
- **CORS**: Backend allows requests from the frontend domain

---

## 2. User Personas

### 2.1 Persona: Budi - The Hobbyist Gardener
**Role:** Customer
**Goals:** Find quality plant seeds for his home gardening hobby
**Pain Points:**
- Hard to find a trustworthy seed shop
- Doesn't know how to care for the seeds he buys
- Worries that seeds will get damaged during shipping

**Needs:**
- A seed catalog with clear photos and descriptions
- A short planting guide on each product
- Order confirmation and shipping tracking

### 2.2 Persona: Sari - The Beginner Farmer
**Role:** Customer
**Goals:** Start growing organic vegetables in her backyard
**Pain Points:**
- Confused about which seeds are suitable for beginners
- Wants to buy multiple seed types at once
- Needs to know harvest time and growing season

**Needs:**
- Search filters by category and difficulty level
- A shopping cart to buy multiple products at once
- Harvest time information on the product page

### 2.3 Persona: Pak Andi - The Shop Admin
**Role:** Shop Admin
**Goals:** Manage the online shop efficiently
**Pain Points:**
- Hassle of recording stock and orders manually
- Difficult to monitor incoming orders
- Updating products takes too much time

**Needs:**
- A dashboard to view orders and stock
- A simple form to add/edit products
- Notifications for new orders

---

## 3. User Stories & Acceptance Criteria

### Epic 1: Authentication & User Management

#### US-001: User Registration
**As a** new prospective buyer
**I want to** register with my email and password
**So that** I can shop in the store

**Acceptance Criteria:**
- [ ] User can register with: name, email, password, phone number
- [ ] Email must be unique in the system
- [ ] Password must be at least 8 characters
- [ ] After registration, user is redirected to the login page
- [ ] Validation errors are clearly displayed for each field

**Priority:** High
**Story Points:** 3

#### US-002: User Login
**As a** registered user
**I want to** log in with my email and password
**So that** I can access my account

**Acceptance Criteria:**
- [ ] User can enter email and password
- [ ] System validates credentials via Laravel Passport
- [ ] Successful login returns an access token (Bearer token)
- [ ] Token is stored on the frontend (httpOnly cookie or localStorage)
- [ ] Failed login displays "Invalid email or password" message
- [ ] Token expires after 24 hours; user must log in again
- [ ] "Forgot password?" link available (optional in MVP)

**Priority:** High
**Story Points:** 2

#### US-003: View & Edit Profile
**As a** user
**I want to** view and update my profile
**So that** my data stays current

**Acceptance Criteria:**
- [ ] Profile displays: name, email, phone number, shipping address
- [ ] User can update: name, phone number, address
- [ ] User cannot change email
- [ ] Changes are saved with success confirmation

**Priority:** Medium
**Story Points:** 2

---

### Epic 2: Product Catalog

#### US-004: View Product List
**As a** customer
**I want to** view the list of plant seeds for sale
**So that** I can choose products to buy

**Acceptance Criteria:**
- [ ] Home page shows a product list (photo, name, price, stock)
- [ ] Each product displays a category badge (Vegetable/Fruit/Ornamental)
- [ ] Product list is paginated (12 products per page)
- [ ] Products with 0 stock are marked "Out of Stock"
- [ ] Clicking a product opens its detail page

**Priority:** High
**Story Points:** 3

#### US-005: Search & Filter Products
**As a** customer
**I want to** search and filter products
**So that** I can find the seeds I need

**Acceptance Criteria:**
- [ ] Search bar to search by product name
- [ ] Filter by category (Vegetables, Fruits, Ornamental Plants, Herbs)
- [ ] Sort by: price (low to high / high to low), newest
- [ ] Search results update in real time
- [ ] "Product not found" message if results are empty

**Priority:** High
**Story Points:** 3

#### US-006: View Product Detail
**As a** customer
**I want to** view product details
**So that** I have complete information before buying

**Acceptance Criteria:**
- [ ] Displays: product photo, name, price, stock, description, category
- [ ] Additional info: planting guide, harvest time, sunlight needs
- [ ] "Add to Cart" button (disabled if stock is 0)
- [ ] Quantity input with +/- buttons (max equals available stock)
- [ ] "Buy Now" button for direct checkout

**Priority:** High
**Story Points:** 3

---

### Epic 3: Shopping Cart & Checkout

#### US-007: Add to Cart
**As a** customer
**I want to** add products to my cart
**So that** I can buy multiple products at once

**Acceptance Criteria:**
- [ ] "Add to Cart" button adds the product to the cart
- [ ] Success notification appears after adding
- [ ] Cart icon displays the item count
- [ ] If the product is already in the cart, quantity increases
- [ ] User must be logged in to add to cart

**Priority:** High
**Story Points:** 3

#### US-008: View & Update Cart
**As a** customer
**I want to** view and update my cart contents
**So that** I can adjust my order before paying

**Acceptance Criteria:**
- [ ] Cart page displays: photo, name, price, quantity, subtotal per item
- [ ] User can change quantity (+/- or input)
- [ ] User can remove items from the cart
- [ ] Total price is calculated automatically
- [ ] "Proceed to Checkout" button is available if the cart is not empty
- [ ] "Cart is empty" message if there are no items

**Priority:** High
**Story Points:** 3

#### US-009: Checkout
**As a** customer
**I want to** complete my order
**So that** my order is processed

**Acceptance Criteria:**
- [ ] Checkout page displays: order summary, shipping address, payment method
- [ ] Shipping address auto-fills from profile (editable)
- [ ] Payment method options: Bank Transfer, COD (Cash on Delivery)
- [ ] Final total = subtotal + shipping cost
- [ ] "Place Order" button processes the order
- [ ] After success, user is redirected to a confirmation page with the order code

**Priority:** High
**Story Points:** 5

---

### Epic 4: Order Management

#### US-010: View Order History
**As a** customer
**I want to** view my order history
**So that** I can track the orders I've placed

**Acceptance Criteria:**
- [ ] Order list displays: order code, date, total, status
- [ ] Order status: Awaiting Payment, Processing, Shipped, Completed, Cancelled
- [ ] Sorted by newest first
- [ ] Clicking an order opens the detail page

**Priority:** High
**Story Points:** 3

#### US-011: View Order Detail
**As a** customer
**I want to** view order details
**So that** I have complete information about the order

**Acceptance Criteria:**
- [ ] Displays: order code, date, product list, shipping address, payment method, total
- [ ] Displays the current order status
- [ ] "Confirm Received" button appears when status is "Shipped"
- [ ] "Cancel Order" button appears when status is "Awaiting Payment"

**Priority:** High
**Story Points:** 3

---

### Epic 5: Admin Management

#### US-012: Admin Login
**As an** admin
**I want to** log in to the admin panel
**So that** I can manage the shop

**Acceptance Criteria:**
- [ ] Admin login page is separate from the customer login
- [ ] Only users with the admin role can access it
- [ ] Successful login redirects to the admin dashboard

**Priority:** High
**Story Points:** 2

#### US-013: Manage Products (CRUD)
**As an** admin
**I want to** add, edit, and delete products
**So that** the catalog is always up to date

**Acceptance Criteria:**
- [ ] Add product form: name, category, price, stock, photo, description, planting info
- [ ] Product photo max 2MB (JPG/PNG)
- [ ] Edit product uses the same form (pre-filled)
- [ ] Delete product requires confirmation
- [ ] Validation: price > 0, stock >= 0, all fields required (except description)

**Priority:** High
**Story Points:** 5

#### US-014: Manage Orders
**As an** admin
**I want to** manage incoming orders
**So that** orders can be processed correctly

**Acceptance Criteria:**
- [ ] List of all orders with status filters
- [ ] Order detail displays buyer and product information
- [ ] Admin can change order status
- [ ] Product stock decreases automatically when an order is placed
- [ ] Stock is restored if an order is cancelled

**Priority:** High
**Story Points:** 4

#### US-015: Admin Dashboard
**As an** admin
**I want to** see a shop summary
**So that** I can know shop performance at a glance

**Acceptance Criteria:**
- [ ] Displays: today's total orders, today's revenue, new orders, low-stock products
- [ ] List of 5 most recent orders
- [ ] List of 5 best-selling products
- [ ] Auto-refresh whenever the page is opened

**Priority:** Medium
**Story Points:** 3

---

## 4. UI/UX Requirements

### 4.1 Design Principles
1. **Simple**: Clean appearance, easy for everyday users to understand
2. **Visual**: Large, attractive product photos
3. **Fast**: Minimal clicks during shopping
4. **Mobile-Friendly**: Optimized for mobile since most users are on phones
5. **Feedback**: Every action provides clear visual confirmation

### 4.2 Key UI Components

#### Navigation
- **Header**: Logo, search bar, cart icon, profile menu
- **Footer**: Shop info, contact, policy links
- **Sidebar (Admin)**: Dashboard, Products, Orders, Settings

#### Product Views
- **Grid View**: Product cards with photo, name, price (primary)
- **Detail View**: Large photo, full info, action buttons

#### Forms
- **Inline Validation**: Immediate feedback on input
- **Loading State**: Loading indicator on submit
- **Confirmation**: Confirmation modal for important actions (delete, cancel)

#### Notifications
- **Toast**: Non-blocking success/error notifications
- **Badge**: Item count on the cart icon

### 4.3 Responsive Considerations
- **Mobile (<768px)**: Single column, bottom navigation, primary priority
- **Tablet (768px-1023px)**: 2-column product grid
- **Desktop (1024px+)**: 3-4 column product grid, persistent sidebar

**Note**: Mobile is the primary target since most customers use phones.

### 4.4 Accessibility Requirements
- Color contrast follows WCAG 2.1 AA
- Alt text for all product photos
- Forms are keyboard navigable
- Minimum font size of 14px

---

## 5. Non-Functional Requirements

### 5.1 Performance
- Home page load: < 3 seconds
- Product list (12 items): < 2 seconds
- Checkout process: < 3 seconds

### 5.2 Reliability
- System uptime: 99% (excluding scheduled maintenance)
- Daily database backup

### 5.3 Security
- Data encrypted in transit (HTTPS)
- Passwords hashed with bcrypt (Laravel default)
- Authentication using Laravel Passport (OAuth2 + Bearer Token)
- Token expires after 24 hours
- Role-based access (customer vs admin) using Laravel middleware
- CSRF protection on sensitive forms
- SQL Injection protection via Eloquent ORM
- XSS protection on the frontend (input sanitization)

### 5.4 Scalability
- Supports 50 concurrent users (initial)
- Supports at least 500 products in the catalog

---

## 6. Success Metrics

### 6.1 Adoption Metrics
| Metric | Target | Measurement |
|--------|--------|-------------|
| New User Registrations | 50/month | Database count |
| Orders per Week | 30+ | Database count |
| Cart-to-Checkout Conversion | 60% | Ratio calculation |

### 6.2 Efficiency Metrics
| Metric | Target | Measurement |
|--------|--------|-------------|
| Checkout Time | < 2 minutes | User timing |
| Admin Add Product Time | < 1 minute | User timing |

### 6.3 Quality Metrics
| Metric | Target | Measurement |
|--------|--------|-------------|
| Completed Orders (not cancelled) | > 90% | Ratio |
| Customer Satisfaction | > 4.0/5.0 | Survey |
| Critical Bugs | < 3/month | Issue tracker |

---

## 7. Release Planning

### Phase 1: MVP (Weeks 1-4)
**Goal**: Core online shop functionality

**Features:**
- US-001 to US-003: Authentication & Profile
- US-004 to US-006: Product catalog
- US-013: Admin add/edit products

**Success Criteria:**
- Users can register, log in, and view products
- Admin can populate the catalog

### Phase 2: Shopping & Checkout (Weeks 5-7)
**Goal**: Customers can complete purchases

**Features:**
- US-007 to US-009: Cart & checkout
- US-010 to US-011: Order history
- US-014: Admin order management

**Success Criteria:**
- End-to-end purchasing flow works
- Admin can process orders

### Phase 3: Polish & Dashboard (Weeks 8-9)
**Goal**: Improved experience and admin visibility

**Features:**
- US-015: Admin dashboard
- US-005: Search & filter
- UI/UX improvements
- Bug fixes

**Success Criteria:**
- Admin has full visibility
- Customers can easily find products
- No critical bugs

---

## 8. Open Questions

1. **Payment**: Should we integrate a payment gateway (Midtrans/Xendit) in MVP, or is manual transfer sufficient?
2. **Shipping**: Should we integrate RajaOngkir or use a flat-rate shipping fee?
3. **Notifications**: Are email/WhatsApp notifications needed for order updates?
4. **Vouchers**: Are voucher/discount features required in MVP?
5. **Product Reviews**: Should customers be able to leave reviews/ratings?

---

## 9. Approval

**Product Owner Approval:**
- [ ] Specification reviewed and approved
- [ ] Scope confirmed
- [ ] Priorities aligned
- [ ] Success metrics agreed upon

**Sign-off:**
| Role | Name | Signature | Date |
|------|------|-----------|------|
| Product Owner | | | |
| Technical Lead | | | |
| Stakeholder | | | |

---

## 10. Appendix

### A. Glossary
- **Customer**: User who buys products
- **Admin**: Shop manager
- **Cart**: Place to store products before checkout
- **COD**: Cash on Delivery (pay on arrival)
- **MVP**: Minimum Viable Product
- **US**: User Story
- **Laravel Passport**: OAuth2 package for API authentication in Laravel
- **Bearer Token**: Authentication token sent in the HTTP Authorization header
- **shadcn/ui**: UI component library built on Radix UI and Tailwind CSS
- **REST API**: HTTP-based API architecture using JSON format

### B. Revision History
| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 0.1 | 2026-04-27 | System | Initial draft |
| 0.2 | 2026-04-27 | System | Renamed app to "Holy Seed", added tech stack (Laravel + Passport, MySQL, Next.js, shadcn, Tailwind) |
| 0.3 | 2026-04-27 | System | Translated full document to English |

---

*End of PRD v01*
