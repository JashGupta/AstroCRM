# 🌌 AstroCRM — Customer Relationship Management for Astrologers

A full-stack CRM web application built to help professional astrologers manage their client relationships, log consulting sessions, track follow-up tasks, and monitor their monthly earnings.

I built this project to solve a real-world problem: helping independent consultants and astrologers organize client records and birth charts (date, time, and place of birth) in one centralized, easy-to-use dashboard.

---

## 🔗 Live Links

*   **Frontend Client:** [https://astro-crm-black.vercel.app/login](https://astro-crm-black.vercel.app/login)
*   **Backend Server API:** [https://astrocrm-z71s.onrender.com](https://astrocrm-z71s.onrender.com)

---

## 🚀 Key Features

*   **🔐 Account Registration & Login:** JWT-based authentication featuring secure access tokens stored in memory and automated token rotation via HTTP-Only refresh token cookies.
*   **📊 Analytics Dashboard:** At-a-glance cards showing active clients, monthly consultations, pending reminders, and total revenue. Interactive charts tracking monthly consultations, revenue trends, and consultation types.
*   **👤 Client Profiles:** Dedicated database for saving client information, birth details (birth date, time, and coordinates), and background history notes.
*   **🔮 Consultation Logs:** Track details of every session including consultation topic (e.g. Birth Chart, Horoscope, Matchmaking, Remedy), duration, billing amount, and payment status (paid, pending, waived).
*   **⏰ Follow-up Reminders:** An automated task management system categorized by priority (low, medium, high) and status (pending, completed, overdue).
*   **📱 Responsive Interface:** Fully mobile-friendly layout built with Tailwind CSS, accommodating mobile, tablet, and desktop views.

---

## ⚙️ Tech Stack

### Frontend
*   **Library:** React 18
*   **Build Tool:** Vite
*   **Styling:** Tailwind CSS
*   **Charts:** Recharts
*   **Icons:** Lucide React
*   **API Client:** Axios (with interceptors for injecting headers and handling 401 logouts)

### Backend
*   **Runtime:** Node.js
*   **Framework:** Express.js
*   **Database:** MongoDB
*   **ODM:** Mongoose
*   **Auth:** JWT (jsonwebtoken) & bcryptjs (password hashing)
*   **Security:** Helmet, CORS, Cookie-Parser, and Express-Validator for form inputs

---

## 📂 Project Structure

```text
AstroCRM/
├── client/                 # React frontend application
│   ├── src/
│   │   ├── app/            # Routes and App providers
│   │   ├── components/     # UI elements (buttons, inputs, layouts)
│   │   ├── context/        # Global Auth and Toast contexts
│   │   ├── features/       # Feature directories (auth, clients, dashboard, follow-ups)
│   │   └── lib/            # Axios API config and utilities
│   └── tailwind.config.js  # Tailwind CSS custom themes
│
└── server/                 # Express backend API
    ├── src/
    │   ├── config/         # MongoDB setup, CORS, and env verification
    │   ├── controllers/    # Route controllers
    │   ├── middleware/     # JWT protection, validate, and error handlers
    │   ├── models/         # Mongoose Schemas (Astrologer, Client, Consultation, etc.)
    │   ├── routes/         # Router declarations
    │   ├── services/       # Core business logic
    │   └── validators/     # Express validation rule files
```

---

## 🛠️ Local Development & Setup

### Prerequisites
*   Node.js (v18.x or higher) installed
*   MongoDB installed and running locally, or a MongoDB Atlas connection string

### 1. Database Configuration
Ensure your local MongoDB instance is running at `mongodb://localhost:27017` or obtain a connection URI from MongoDB Atlas.

### 2. Backend Server Setup
1.  Navigate to the server directory:
    ```bash
    cd server
    ```
2.  Install dependencies:
    ```bash
    npm install
    ```
3.  Configure environment variables by creating a `.env` file:
    ```bash
    cp .env.example .env
    ```
    Configure the following values inside `.env`:
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
4.  Start the backend development server:
    ```bash
    npm run dev
    ```

### 3. Frontend Client Setup
1.  Open a new terminal and navigate to the client directory:
    ```bash
    cd client
    ```
2.  Install dependencies:
    ```bash
    npm install
    ```
3.  Configure environment variables by creating a `.env` file:
    ```bash
    cp .env.example .env
    ```
    Ensure it points to your backend URL:
    ```env
    VITE_API_URL=http://localhost:5000/api/v1
    ```
4.  Start the Vite local development server:
    ```bash
    npm run dev
    ```
5.  Open `http://localhost:5173` in your browser.

---

## ⚡ Challenges Faced

*   **Secure Session Management:** Balancing security with user experience was tricky. I implemented a short-lived `accessToken` in memory and a secure, `httpOnly` `refreshToken` cookie. Writing the Axios request interceptors to automatically refresh expired sessions without kicking the user out took some trial and error.
*   **MongoDB Analytics Aggregations:** Creating the charts on the dashboard required combining records from multiple collections (Clients, Consultations, and Follow-ups). I had to learn how to write complex MongoDB aggregation pipelines (`$facet`, `$group`, and `$lookup`) to retrieve monthly stats and group totals efficiently in single database requests.
*   **Handling Timezone Offsets:** Clients book consultations and set follow-ups in their local time, but servers store datetimes in UTC. Resolving bugs where date pickers shifted dates by ±1 day depending on local timezone offsets was a challenging debugging exercise.

---

## 🔮 Future Enhancements

1.  **💬 WhatsApp & SMS Alerts:** Auto-send consultation booking confirmations and upcoming callback notifications to clients.
2.  **💳 Payment Gateway Integration:** Integrate Stripe or Razorpay to handle booking payments and automatically mark invoices as paid in the database.
3.  **📅 Google Calendar Sync:** Sync follow-ups and consultation schedules with the astrologer's personal Google Calendar.
4.  **📑 Birth Chart PDF Generator:** Add a feature that automatically generates a basic PDF layout containing birth details to email to clients.

---

## ✍️ Author

*   **Jash Gupta**
    *   GitHub: [@JashGupta](https://github.com/JashGupta)
    *   Project: AstroCRM Showcase
    *   Email: jash@example.com
