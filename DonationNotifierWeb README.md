# Donation App — Web Platform & REST API

> A full-stack web application that serves as the management dashboard, public-facing website, and REST API for the Donation Notifier ecosystem — built for live streaming content creators.

---

## 📌 Overview

**DonationAppWeb** is the central hub of the Donation Notifier platform. It provides:

1. **A public marketing website** — landing page, feature showcase, download page, legal documents, and community section.
2. **A creator dashboard** — a protected settings panel where authenticated users manage overlays, view donation history, configure plans, and control every aspect of their streaming setup.
3. **Browser-based OBS overlay widgets** — standalone, chrome-free pages designed to be added directly as browser sources inside OBS Studio or any streaming software.
4. **A REST API backend** — an Express.js server that handles authentication, user management, Razorpay payments, Firebase integrations, and data persistence via MongoDB.

---

## ✨ Key Features

### 🌐 Public Website
- Animated **Hero Section** with live community user avatars
- **Ticker / scrolling banner** highlighting key platform benefits
- **Mission Section** explaining the platform's purpose
- **Features Section** with interactive cards and descriptions
- **How It Works** step-by-step guide
- **Carousel / Gallery** showcasing overlay widgets in action
- **Community Section** — live data from the backend showing real connected creators and user reviews
- **Call-to-Action** section with sign-up prompts
- **Download Page** — direct APK download for the Android companion app (v1.0.23, ~60 MB)
- **Legal Pages** — Privacy Policy, Terms & Conditions, Refund Policy
- **Contact Us** page with inquiry form
- **Stream Overlay Demo** — interactive demo of available widget types

### 🎛️ Creator Dashboard (Protected)
- Google OAuth 2.0 sign-in with Firebase Authentication
- **Dashboard Tab** — quick overview of active overlays, membership status, and setup progress
- **History Tab** — paginated donation transaction history with filtering
- **Recharge / Billing Tab** — subscription plan selection and Razorpay payment flow
- Setup progress tracker to guide new users through configuration steps

### 📺 OBS Overlay Widgets
All widget pages are served at `/widget/:userID/...` routes, designed to be loaded directly as **Browser Sources** in OBS Studio. Each widget connects to the real-time Socket server and updates live on stream:

| Widget | Route | Description |
|--------|-------|-------------|
| Today's Donations | `/widget/:userID` | Running total of today's donations |
| Today's Target | `/widget/todaytarget/:userID` | Progress bar toward a donation goal |
| Top Donor List | `/widget/toplist/:userID` | Rolling banner of top donors |
| Sponsor Card | `/widget/sponsorcard/:userID` | Individual sponsor highlight card |
| Sponsor Banner | `/widget/sponsorbanner/:userID` | Wide sponsor logo banner |
| Membership Count | `/widget/membershipcount/:userID` | Live membership counter overlay |
| Cricket Scoreboard | `/widget/scoreboard/:userID` | Live cricket match score (via Cricbuzz) |
| Alert Widget | `/widget/alertwidget/:userID` | Animated donation alert popup |
| Top Donation Names | `/widget/topdonationlistname/:userID` | Animated list of top donor names |
| Challenge Text | `/widget/challenge/:userID` | Scrolling challenge/goal text |
| Combined Widget | `/widget/combined/:userID` | Multi-info combined overlay |

### 🛡️ Admin Panel
- Admin-only protected routes (`/admin`, `/admin/library`)
- **Library Portal** — manage media assets uploaded by users
- **Overlay Updates** — push overlay configuration changes to connected users in real time

### 💳 Payments & Subscriptions
- Razorpay payment gateway integration (server-side order creation + client-side checkout)
- Subscription plan management with billing history
- Webhook-based payment verification

### 🔐 Security
- JWT-based session management with HTTP-only cookies
- `bcryptjs` password hashing
- `helmet` for secure HTTP headers
- `express-rate-limit` for API rate limiting
- Firebase Admin SDK for token verification
- CORS policy enforcement

### 🤖 Web Scraping
- Puppeteer (with stealth plugin) for automated web data collection
- Cheerio for fast HTML parsing (cricket score data from Cricbuzz)
- `node-cron` for scheduled background scraping jobs

---

## 🛠️ Technology Stack

### Frontend (React + Vite)
| Layer | Technology |
|-------|-----------|
| Framework | React 18 + Vite |
| Language | JavaScript (JSX) |
| Routing | React Router DOM v6 |
| Animation | Framer Motion + React Spring |
| Icons | React Icons |
| UI Components | Material Tailwind (supplemental) |
| Authentication | Firebase JS SDK |
| Realtime | Socket.IO Client |
| HTTP Client | Axios |
| Styling | Vanilla CSS + CSS custom properties |
| Fonts | Google Fonts (Bricolage Grotesque, DM Sans) |

### Backend (Node.js + Express)
| Layer | Technology |
|-------|-----------|
| Runtime | Node.js (ESM) |
| Framework | Express.js |
| Database | MongoDB via Mongoose |
| Authentication | Firebase Admin SDK + JWT |
| Payments | Razorpay SDK |
| Realtime | Socket.IO |
| Web Scraping | Puppeteer + Cheerio |
| Scheduling | node-cron |
| Security | Helmet, bcryptjs, express-rate-limit |
| Deployment | Vercel |

---

## 🏗️ Project Structure

```
DonationAppWeb/
├── client/                    # React + Vite frontend
│   └── src/
│       ├── pages/             # Route-level page components
│       │   ├── Home.jsx
│       │   ├── DownloadApp.jsx
│       │   ├── StreamOverlayDemo.jsx
│       │   ├── PrivacyPolicy.jsx
│       │   └── admin/         # Admin-only pages
│       ├── component/
│       │   ├── home/          # Landing page sections (Hero, Features, etc.)
│       │   ├── dashboard/     # Creator dashboard tabs
│       │   ├── widget/        # OBS overlay widget components
│       │   │   └── overlays/  # Overlay-specific sub-widgets
│       │   ├── payments/      # Payment gateway components
│       │   └── themes/        # Theme-related UI components
│       ├── layouts/           # PublicLayout, WidgetLayout wrappers
│       ├── context/           # React Context providers (Auth, LoginModal)
│       ├── hooks/             # Custom React hooks
│       ├── services/          # API service modules
│       └── wrapper/           # OverlayWrapper, SocketWrapper HOCs
│
└── server/                    # Express.js REST API
    ├── models/                # Mongoose schemas
    │   ├── user.model.js
    │   ├── alert.model.js
    │   ├── token.model.js
    │   └── socketHistory.model.js
    ├── routes/                # API route definitions
    │   ├── user.routes.js
    │   ├── donation.routes.js
    │   ├── razorpay.routes.js
    │   ├── community.routes.js
    │   ├── library.routes.js
    │   └── admin.routes.js
    ├── controllers/           # Route handler logic
    ├── services/              # Business logic services
    ├── socket/                # Socket.IO server setup
    ├── scripts/               # Utility and maintenance scripts
    └── index.js               # Server entry point
```

---

## 📸 Screenshots

> _Add screenshots of your web platform here._

| Landing Page | Creator Dashboard | Overlay Widgets | Download Page |
|-------------|-------------------|-----------------|---------------|
| ![Home](docs/home.png) | ![Dashboard](docs/dashboard.png) | ![Widgets](docs/widgets.png) | ![Download](docs/download.png) |

---

## 🔗 Related Projects

This repository is part of a three-repository ecosystem:

| Repository | Description |
|-----------|-------------|
| [DonationNotifierApp](../DonationNotifierApp) | React Native Android app for creators |
| **DonationAppWeb** ← You are here | Web dashboard, overlay widgets, and REST API |
| [DonationAppSocket](../DonationAppSocket) | Dedicated WebSocket & real-time event server |

---

## ⚙️ Requirements

- **Node.js**: 18 or higher
- **MongoDB** instance (local or Atlas)
- Firebase project (Auth, Firestore, Storage, Admin SDK)
- Razorpay account (for payment processing)
- Active instance of **DonationAppSocket** for real-time overlay events

---

## 🚀 Deployment

The application is deployed on **Vercel** using the configuration defined in `vercel.json`. The frontend is built with Vite and served statically; the Express backend runs as a Vercel serverless function.

Build command:
```
npm install && npm install --prefix client && npm run build --prefix client
```

---

## 👤 Author

**Imran Nazeer S** — Full Stack Developer  
Built with ❤️ for the creator community.

---

## 📄 License

Private — All rights reserved.
