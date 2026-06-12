# 🌌 AstroCRM — Astrologer Customer Relationship Management

[![React](https://img.shields.io/badge/React-18.3-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-4.21-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-8.0-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)

A modern, full-stack Customer Relationship Management (CRM) system customized specifically for professional astrologers. **AstroCRM** empowers astrologers to seamlessly manage their client relationships, track consultations, monitor scheduled follow-ups, and get detailed visual analysis of their revenue growth and business metrics.

This repository is structured for easy deployment, scalability, and code readability. It is highly suitable for university projects, recruiter evaluations, internship portfolios, and open-source contributions.

---

## 🔗 Live Deployments

*   **Frontend Dashboard (Vercel):** [https://astro-crm-black.vercel.app/login](https://astro-crm-black.vercel.app/login)
*   **API Server (Render):** [https://astrocrm-z71s.onrender.com](https://astrocrm-z71s.onrender.com)

---

## 📸 Screenshots

> *Below are placeholders for the visual interface of AstroCRM. Replace these with actual images when showcasing in your portfolio.*

| 📊 Analytics Dashboard | 👤 Client Management |
| :---: | :---: |
| ![Dashboard Placeholder](https://via.placeholder.com/800x450/1e1e24/a78bfa?text=AstroCRM+Dashboard+Charts) | ![Client Details Placeholder](https://via.placeholder.com/800x450/1e1e24/a78bfa?text=Client+Directory+and+Kundli+Data) |
| *Visual analytics charts for monthly earnings, consultation distributions, and pending reminders.* | *Directory of clients featuring advanced search filters, tags, and birth charts.* |

---

## ✨ Features

*   **🔐 User Authentication (Secure JWT Rotation):** Hashed passwords (using `bcryptjs`) and secure login/registration workflows. Implements a secure dual-token system (short-lived `accessToken` in local memory and rotation-enabled `refreshToken` in HTTP-Only cookies).
*   **📊 Dashboard Analytics:** Displays high-level Key Performance Indicators (KPIs) like active clients, monthly revenue growth, total consultations, and overdue follow-ups. Built-in interactive data visualizations using `recharts` for tracking trends.
*   **👤 Client Management:** Dedicated customer profiles containing detailed astrological metadata: birth dates, exact birth times, birth coordinates (place of birth, country, latitude/longitude), custom notes, and automatic consultation counters.
*   **🔮 Consultation Management:** Track consulting sessions categorized by type (e.g., Birth Chart reading, Horoscope, Matchmaking, Remedy prescriptions). Maintain histories of pricing, billing statuses (`paid`, `pending`, `waived`), session durations, notes, and specific recommendations.
*   **⏰ Follow-up Tracking:** Reminders automatically marked as `overdue` or `pending` based on due dates. Prioritization metrics (`low`, `medium`, `high`) ensure critical client issues are addressed on time.
*   **📈 Revenue Tracking:** Comprehensive chart summaries capturing total income, monthly comparison logs, and month-over-month (MoM) revenue growth trends.
*   **📱 Responsive UI Design:** Handcrafted using React 18, Vite, and Tailwind CSS. The interface adapts cleanly to desktop, tablet, and mobile browsers.
*   **🛡️ Protected Routes:** Secure client-side routing using `react-router-dom` v6, backed by server-side verification middleware.

---

## ⚙️ Tech Stack

### Frontend
*   **Framework:** React 18 (Vite-powered, SPA architecture)
*   **Styling:** Tailwind CSS (extended custom brand color palette)
*   **Icons:** Lucide React
*   **Data Visualization:** Recharts
*   **HTTP Client:** Axios (configured with request/response interceptors)

### Backend
*   **Runtime Environment:** Node.js (>= 18.0.0)
*   **Framework:** Express.js (RESTful API architecture)
*   **Database ODM:** Mongoose (MongoDB Object Modeling)
*   **Security & Helpers:** Helmet, CORS, Cookie-Parser, Morgan, Express-Validator
*   **Authentication:** JSON Web Tokens (JWT) + Bcryptjs

### Database
*   **Engine:** MongoDB (Document-oriented NoSQL database)
*   **Storage Type:** Multi-tenant isolation scoped per astrologer profile

---

## 🏗️ Project Architecture

AstroCRM implements a layered multi-tier architecture where the user interface interacts with an isolated backend service through a secure REST API.

```
          ┌──────────────────┐
          │      User        │
          └────────┬─────────┘
                   │
                   │ HTTP Requests / UI Interaction
                   ▼
          ┌──────────────────┐
          │  React Frontend  │ (Client-side Router, Axios Interceptors)
          └────────┬─────────┘
                   │
                   │ REST API Calls (Bearer JWT in Authorization Header)
                   ▼
          ┌──────────────────┐
          │   Express API    │ (Validation, Router, Controller, Services)
          └────────┬─────────┘
                   │
                   │ Mongoose ODM (Queries & Aggregations)
                   ▼
          ┌──────────────────┐
          │     MongoDB      │ (Collections scoped by Astrologer ObjectId)
          └──────────────────┘
```

### Flow of Execution:
1. **Request:** The user triggers an action in the React client. Axios intercepts the request to inject the JWT `Authorization` header.
2. **Security & Validation:** Express passes the request through security headers (`helmet`), validates inputs (`express-validator`), and checks token validity via `auth.middleware`.
3. **Controller & Service Layer:** The matching route controller captures the request, delegating the core business rules and query formulations to the Service layer.
4. **Data Layer:** Mongoose connects to MongoDB, utilizing indexes to query datasets.
5. **Response:** Data is returned to the user in a standardized JSON envelope structure.

---

## 📂 Folder Structure

```
AstroCRM/
├── client/                     # Frontend Application
│   ├── src/
│   │   ├── app/                # Global providers and routing setup
│   │   │   ├── providers.jsx
│   │   │   └── router.jsx
│   │   ├── components/         # Reusable presentation components
│   │   │   ├── feedback/       # Spinner, EmptyState, ErrorState
│   │   │   ├── layout/         # Header, Sidebar, PageLayout, ProtectedRoute
│   │   │   └── ui/             # Avatar, Button, Card, Input, Modal, Select
│   │   ├── constants/          # Application-wide static options
│   │   ├── context/            # Global React Contexts (AuthContext, ToastContext)
│   │   ├── features/           # Feature modules (Domain-driven structure)
│   │   │   ├── auth/           # Login, Registration pages and services
│   │   │   ├── clients/        # Client list, details, and editor
│   │   │   ├── consultations/  # Appointment form and list pages
│   │   │   ├── dashboard/      # Analytics dashboard charts
│   │   │   └── follow-ups/     # Reminders and action items
│   │   ├── hooks/              # Custom shared hooks
│   │   ├── lib/                # API wrapper configuration & utilities
│   │   ├── index.css           # Global CSS and Tailwind directives
│   │   └── main.jsx            # Application entry point
│   ├── tailwind.config.js      # Tailwind style system configurations
│   └── vite.config.js          # Vite build tool setup
│
├── server/                     # Backend API Server
│   ├── src/
│   │   ├── config/             # DB connection, CORS, & env validators
│   │   ├── controllers/        # HTTP controllers (receives and responds)
│   │   ├── middleware/         # Auth guards, errors, & validation middleware
│   │   ├── models/             # Mongoose schemas & life-cycle hooks
│   │   ├── routes/             # REST endpoints split by resource
│   │   ├── services/           # Reusable core business logic layer
│   │   ├── utils/              # Custom error helpers and pagination calculators
│   │   ├── validators/         # Input sanitization and rule definitions
│   │   ├── app.js              # Express app definition & mid-level setup
│   │   └── server.js           # Server runner and listener
│   └── package.json            # Server-side scripts and package dependencies
```

---

## 🔐 Authentication Flow

AstroCRM implements standard JWT-based authorization utilizing access tokens combined with secure refresh token rotation to minimize database lookups and prevent CSRF/XSS vectors.

```
┌──────────┐                 ┌──────────┐                 ┌──────────┐
│  Client  │                 │   API    │                 │ Database │
└────┬─────┘                 └────┬─────┘                 └────┬─────┘
     │                            │                            │
     │ ─── 1. Login (Email/Pass) ─>                            │
     │                            │ ─── 2. Validate Credentials ─>
     │                            │ <── 3. Astrologer Found ────
     │                            │                            │
     │                            │ ─── 4. Save RefreshToken ──>
     │                            │ <── 5. Token Saved ────────
     │ <── 6. AccessToken (JSON) ─│                            │
     │        + RefreshToken (Cookie)                          │
     │                            │                            │
     ├────────────────────────────┤                            │
     │                            │                            │
     │ ─── 7. API Call (Bearer) ─>│                            │
     │                            │ ─── 8. Local Verification ─>
     │ <── 9. Respond with Data ──│                            │
     │                            │                            │
```

1. **Authentication:** Astrologer logs in. The backend issues a short-lived JSON Web Token (`accessToken`, expires in 15m) returned in the response body, and a long-lived `refreshToken` (expires in 7d) configured as an `httpOnly`, secure, same-site cookie.
2. **Accessing Protected Routes:** The frontend stores the `accessToken` in local memory and appends it as a `Bearer` token inside the `Authorization` header for all requests.
3. **Session Refresh:** When the `accessToken` expires, the frontend calls the token rotation route. The server checks the secure cookie, validates it against the stored session in the `RefreshToken` collection, and issues a new `accessToken`.

---

## 💾 Database Models

### 1. Astrologer (User)
```javascript
{
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true, select: false },
  phone: { type: String, default: null },
  specializations: { type: [String], default: [] },
  profileImage: { type: String, default: null },
  isActive: { type: Boolean, default: true },
  settings: {
    timezone: { type: String, default: 'Asia/Kolkata' },
    defaultConsultationDuration: { type: Number, default: 60 },
    currency: { type: String, default: 'INR' }
  }
}
```

### 2. Client
```javascript
{
  astrologerId: { type: ObjectId, ref: 'Astrologer', required: true, index: true },
  name: { type: String, required: true },
  email: { type: String, default: null },
  phone: { type: String, required: true },
  gender: { type: String, enum: ['male', 'female', 'other'], default: null },
  dateOfBirth: { type: Date, default: null },
  timeOfBirth: { type: String, default: null }, // HH:mm format
  placeOfBirth: {
    city: { type: String, default: null },
    state: { type: String, default: null },
    country: { type: String, default: null },
    latitude: { type: Number, default: null },
    longitude: { type: Number, default: null }
  },
  tags: { type: [String], default: [] },
  status: { type: String, enum: ['lead', 'active', 'inactive'], default: 'lead' },
  source: { type: String, default: null },
  notes: { type: String, default: null },
  totalConsultations: { type: Number, default: 0 },
  lastConsultationAt: { type: Date, default: null },
  isDeleted: { type: Boolean, default: false, index: true }
}
```
*   **Index:** Compound unique index on `{ astrologerId: 1, phone: 1 }` under soft-delete filter condition `{ isDeleted: false }`.

### 3. Consultation
```javascript
{
  astrologerId: { type: ObjectId, ref: 'Astrologer', required: true, index: true },
  clientId: { type: ObjectId, ref: 'Client', required: true, index: true },
  consultationDate: { type: Date, required: true },
  consultationType: { type: String, enum: ['birth_chart', 'horoscope', 'matchmaking', 'remedy', 'general'], required: true },
  duration: { type: Number, required: true }, // in minutes
  amount: { type: Number, default: 0 },
  paymentStatus: { type: String, enum: ['pending', 'paid', 'waived'], default: 'pending' },
  notes: { type: String, default: null },
  recommendations: { type: String, default: null },
  nextFollowUpDate: { type: Date, default: null },
  status: { type: String, enum: ['scheduled', 'completed', 'cancelled', 'no_show'], default: 'scheduled' },
  isDeleted: { type: Boolean, default: false, index: true }
}
```

### 4. FollowUp
```javascript
{
  astrologerId: { type: ObjectId, ref: 'Astrologer', required: true, index: true },
  clientId: { type: ObjectId, ref: 'Client', required: true, index: true },
  consultationId: { type: ObjectId, ref: 'Consultation', default: null },
  title: { type: String, required: true },
  description: { type: String, default: null },
  dueDate: { type: Date, required: true },
  priority: { type: String, enum: ['low', 'medium', 'high'], default: 'medium' },
  status: { type: String, enum: ['pending', 'completed', 'overdue', 'cancelled'], default: 'pending' },
  completionNotes: { type: String, default: null },
  completedAt: { type: Date, default: null },
  isDeleted: { type: Boolean, default: false, index: true }
}
```

---

## 📡 API Overview

All API endpoints are prefixed with `/api/v1` and return standardized JSON responses:
```json
{
  "success": true,
  "message": "Information status text",
  "data": { ... }
}
```

| HTTP Method | Endpoint | Description | Guarded by Auth | Validation Rules |
| :--- | :--- | :--- | :---: | :--- |
| **POST** | `/auth/register` | Register a new astrologer | ❌ No | Validate name, valid email format, min 8-char password |
| **POST** | `/auth/login` | Login and receive tokens | ❌ No | Email required, password required |
| **GET** | `/auth/me` | Fetch active profile | 🔑 Yes | None |
| **GET** | `/dashboard/stats` | Retrieve KPI card values | 🔑 Yes | None |
| **GET** | `/dashboard/charts` | Retrieve monthly aggregation logs | 🔑 Yes | None |
| **POST** | `/clients` | Create a client profile | 🔑 Yes | Validate name, phone format, email, gender, coordinates |
| **GET** | `/clients` | List clients (paginated/filtered) | 🔑 Yes | Page, limit, search parameters, client status checks |
| **GET** | `/clients/:id` | Fetch specific client details | 🔑 Yes | Validate MongoDB ID |
| **PATCH** | `/clients/:id` | Update client profile details | 🔑 Yes | Validate optional update parameters |
| **DELETE** | `/clients/:id` | Soft-delete a client | 🔑 Yes | Validate MongoDB ID |
| **POST** | `/consultations` | Schedule a consultation | 🔑 Yes | Client existence check, duration, type, amount, date |
| **GET** | `/consultations` | List consultations | 🔑 Yes | Filter by date limits, pagination |
| **PATCH** | `/consultations/:id` | Update consultation details | 🔑 Yes | Validate MongoDB ID & status |
| **GET** | `/followups/upcoming` | Fetch upcoming reminders | 🔑 Yes | None |
| **GET** | `/followups/overdue` | Fetch past-due reminders | 🔑 Yes | None |
| **PATCH** | `/followups/:id/complete`| Complete a follow-up task | 🔑 Yes | Requires completion notes |

---

## 🚀 Setup & Installation Instructions

### Prerequisites
*   [Node.js](https://nodejs.org/) installed (v18.x or higher recommended)
*   [MongoDB](https://www.mongodb.com/try/download/community) server running locally or a [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) cloud URI.

### 1. MongoDB Configuration
Make sure your MongoDB server is online. If you are using local MongoDB, it typically runs on `mongodb://127.0.0.1:27017`. Ensure you create a database (e.g., `astrologer-crm`).

---

### 2. Backend Setup
1.  Navigate to the server directory:
    ```bash
    cd server
    ```
2.  Install dependencies:
    ```bash
    npm install
    ```
3.  Configure your environment variables:
    Create a `.env` file from the example:
    ```bash
    cp .env.example .env
    ```
    Open `.env` and configure:
    ```env
    PORT=5000
    NODE_ENV=development
    MONGODB_URI=mongodb://localhost:27017/astrologer-crm
    JWT_ACCESS_SECRET=your_super_secret_access_key
    JWT_REFRESH_SECRET=your_super_secret_refresh_key
    JWT_ACCESS_EXPIRES_IN=15m
    JWT_REFRESH_EXPIRES_IN=7d
    CORS_ORIGIN=http://localhost:5173
    ```
4.  Start the development server:
    ```bash
    npm run dev
    ```
    The server should now start on `http://localhost:5000`.

---

### 3. Frontend Setup
1.  Open a new terminal window and navigate to the client folder:
    ```bash
    cd client
    ```
2.  Install dependencies:
    ```bash
    npm install
    ```
3.  Configure environment variables:
    Create a `.env` file:
    ```bash
    cp .env.example .env
    ```
    Verify it contains:
    ```env
    VITE_API_URL=http://localhost:5000/api/v1
    ```
4.  Launch the Vite development server:
    ```bash
    npm run dev
    ```
    Open your browser and navigate to `http://localhost:5173`.

---

## ☁️ Deployment Instructions

### API Server (e.g., Render)
1.  Create a web service pointing to your repository.
2.  Set the **Root Directory** to `server`.
3.  Set the **Build Command** to:
    ```bash
    npm install
    ```
4.  Set the **Start Command** to:
    ```bash
    npm start
    ```
5.  Add all environment variables defined in your backend `.env` file under environment variables settings (make sure to set `NODE_ENV` to `production` and update the `CORS_ORIGIN` to point to your client URL).

### Frontend (e.g., Vercel)
1.  Create a project in Vercel importing this repository.
2.  Set the **Root Directory** to `client`.
3.  Select **Vite** as the framework preset (it will automatically configure build settings to `npm run build` and output directory to `dist`).
4.  Add the environment variable `VITE_API_URL` pointing to your deployed API server URL (e.g., `https://astrocrm-z71s.onrender.com/api/v1`).
5.  Deploy the application. The `vercel.json` rewrite configuration handles React SPA router configurations.

---

## 🔮 Future Improvements

1.  **💬 Automated Messaging:** Integration with WhatsApp Business API and Twilio SMS services for automated reminders when a client's `nextFollowUpDate` is approaching.
2.  **💳 Online Payment Gateways:** Direct billing system integrations (e.g., Stripe, Razorpay) to automatically send custom invoices and update the consultation payment status upon successful payment.
3.  **🗺️ Detailed Kundli API Integrations:** Auto-calculating planetary transits, birth charts, and compatibility values inside the client's profile page using standard astrology APIs.
4.  **🌐 Multi-language Support:** Add support for regional languages to cater to a broader client base.
5.  **📅 Calendar Syncing:** Bidirectional synchronization with Google Calendar and Outlook Calendar for schedules and follow-up activities.

---

## ✍️ Author

*   **Jash Gupta**
    *   GitHub: [@JashGupta](https://github.com/JashGupta)
    *   Portfolio: AstroCRM Project Showcase
    *   Email: jash@example.com *(replace with actual contact)*

---
*Developed with dedication to simplify consulting operations for astrologers.*
