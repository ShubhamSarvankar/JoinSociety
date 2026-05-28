# Join Society

A full-stack e-commerce platform featuring authentication, product management, cart and order workflows, Stripe payments, analytics, and admin tools. Built with a modern JavaScript stack and optimized for performance and scalability.

---

## Tech Stack

### Frontend

* **React 18 (Vite)** – Fast, modern frontend build setup with HMR
* **JavaScript (ES6+)**
* **CSS + Tailwind CSS** – Utility-first styling
* **Axios** – API communication layer
* **Zustand** – Lightweight state management (cart, user, products)
* **React Router DOM v7** – Client-side routing with `<Routes>` and `<Route>`
* **Framer Motion** – Animations and page transitions
* **Recharts** – Analytics dashboard charts
* **react-hot-toast** – Toast notifications
* **react-confetti** – Post-purchase success animation
* **lucide-react** – Icon library

### Backend

* **Node.js + Express.js** – REST API server
* **MongoDB + Mongoose** – NoSQL database and schema modeling
* **JWT Authentication** – Secure user auth via HTTP-only cookies
* **Middleware architecture** – Auth and request handling

### Infrastructure & Services

* **Redis (ioredis)** – Caching layer for performance optimization
* **Cloudinary** – Image upload and media management
* **Stripe** – Full checkout session and payment intent processing

---

## Key Features

### User Features

* User authentication (signup/login) with HTTP-only cookie sessions
* Browse products by category
* Product detail pages and modal views
* Add/remove items from cart
* Address management
* Stripe-powered checkout with coupon support
* Purchase success and cancel flows
* Profile page with order history, coupons, and login/security settings (email + password update)

### Admin Features

* Product creation and management (with Cloudinary image upload)
* Coupon creation and management
* Order tracking
* Analytics dashboard (daily sales, revenue, user/product counts via Recharts)
* Security/account settings tab

### System Features

* Secure API with JWT auth middleware (cookie-based)
* Modular backend with separate controllers, routes, models, and lib integrations
* Redis caching to reduce database load
* Stripe Checkout Session creation and webhook-style success handling
* Production mode serves Vite-built frontend from `frontend/build`

---

## Project Structure

```
join-society/
│
├── backend/
│   ├── controllers/
│   │   ├── analytics.controller.js
│   │   ├── auth.controller.js
│   │   ├── cart.controller.js
│   │   ├── coupon.controller.js
│   │   ├── order.controller.js
│   │   ├── payment.controller.js
│   │   └── product.controller.js
│   ├── models/
│   │   ├── address.model.js
│   │   ├── coupon.model.js
│   │   ├── order.model.js
│   │   ├── product.model.js
│   │   └── user.model.js
│   ├── routes/
│   │   ├── analytics.route.js
│   │   ├── auth.route.js
│   │   ├── cart.route.js
│   │   ├── coupon.route.js
│   │   ├── order.route.js
│   │   ├── payment.route.js
│   │   └── product.route.js
│   ├── middleware/
│   │   └── auth.middleware.js
│   ├── lib/
│   │   ├── cloudinary.js
│   │   ├── db.js
│   │   ├── redis.js
│   │   └── stripe.js
│   └── server.js
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── AnalyticsTab.jsx
│   │   │   ├── CartItem.jsx
│   │   │   ├── CategoryItem.jsx
│   │   │   ├── CouponsTab.jsx
│   │   │   ├── CreateCouponForm.jsx
│   │   │   ├── CreateProductForm.jsx
│   │   │   ├── FeaturedProducts.jsx
│   │   │   ├── GiftCouponCard.jsx
│   │   │   ├── LoadingSpinner.jsx
│   │   │   ├── Navbar.jsx
│   │   │   ├── OrderHistoryTab.jsx
│   │   │   ├── OrderSummary.jsx
│   │   │   ├── PeopleAlsoBought.jsx
│   │   │   ├── ProductCard.jsx
│   │   │   ├── ProductDetails.jsx
│   │   │   ├── ProductDetailsModal.jsx
│   │   │   ├── ProductsList.jsx
│   │   │   └── SecurityTab.jsx
│   │   ├── pages/
│   │   │   ├── AddressPage.jsx
│   │   │   ├── AdminPage.jsx
│   │   │   ├── CartPage.jsx
│   │   │   ├── CategoryPage.jsx
│   │   │   ├── HomePage.jsx
│   │   │   ├── LoginPage.jsx
│   │   │   ├── ProfilePage.jsx
│   │   │   ├── PurchaseCancelPage.jsx
│   │   │   ├── PurchaseSuccessPage.jsx
│   │   │   └── SignUpPage.jsx
│   │   ├── stores/
│   │   │   ├── useCartStore.js
│   │   │   ├── useProductStore.js
│   │   │   └── useUserStore.js
│   │   ├── lib/
│   │   │   └── axios.js
│   │   └── App.jsx
│   └── index.html
│
└── package.json
```

---

## API Routes

All routes are prefixed with `/api`.

| Prefix | Description |
|---|---|
| `/api/auth` | Signup, login, logout, profile, email/password update |
| `/api/products` | Product CRUD, category filtering, featured products |
| `/api/cart` | Get cart, add/remove items, update quantity |
| `/api/coupons` | Get, validate, create, and toggle coupons |
| `/api/payments` | Create Stripe checkout session, handle success |
| `/api/analytics` | Aggregate sales, revenue, user, and product data |
| `/api/orders` | Fetch user order history |

---

## Frontend Routes

| Path | Component | Access |
|---|---|---|
| `/` | `HomePage` | Public |
| `/signup` | `SignUpPage` | Guest only |
| `/login` | `LoginPage` | Guest only |
| `/category/:category` | `CategoryPage` | Public |
| `/products/:id` | `ProductDetails` | Public |
| `/cart` | `CartPage` | Authenticated |
| `/address` | `AddressPage` | Authenticated |
| `/profile` | `ProfilePage` | Authenticated |
| `/purchase-success` | `PurchaseSuccessPage` | Authenticated |
| `/purchase-cancel` | `PurchaseCancelPage` | Authenticated |
| `/secret-dashboard` | `AdminPage` | Admin only |

---

## Performance & Optimization

* Redis caching reduces database load on hot paths
* Zustand avoids heavy global re-renders
* Vite enables fast frontend builds and HMR
* Modular backend ensures maintainability and scalability
* Recharts used for lightweight analytics rendering

---

## Setup & Installation

### Prerequisites

* Node.js 16+
* MongoDB
* Redis (optional but recommended)

### Install & Run

```bash
# Install all dependencies (root + frontend)
npm install
npm install --prefix frontend

# Run backend (from root)
npm run dev

# Run frontend (from frontend/)
cd frontend && npm run dev
```

### Production Build

```bash
npm run build
# Serves frontend/build via Express in production mode
```

> **Note:** Vite outputs to `dist` by default. The production server expects `frontend/build` — ensure `vite.config.js` sets `build.outDir` to `build` or update the path in `server.js`.

---

## Environment Variables

Create a `.env` file in the project root (or `backend/`) with:

```
PORT=5000
NODE_ENV=development

MONGO_URI=
JWT_SECRET=

REDIS_URL=

CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=

STRIPE_SECRET_KEY=
CLIENT_URL=http://localhost:5173
```

---

## Summary

Join Society is a **production-relevant MERN application enhanced with Redis, Stripe, and Cloudinary**, demonstrating:

* Modular Express backend with full auth, payment, and admin flows
* Fast Vite + React frontend with Zustand state management
* Real-world integrations: Stripe Checkout, Cloudinary image uploads, Redis caching
* Complete user journey: browse → cart → checkout → order history
* Admin tooling: product/coupon management and a live analytics dashboard