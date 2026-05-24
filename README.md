<div align="center">
<img src="https://img.shields.io/badge/Donation_Notifier-Platform_Showcase-6C3AF5?style=for-the-badge" alt="Donation Notifier Platform" />
# 🎙️ Donation Notifier Platform
### Real-time donation alerts & live stream overlays for content creators
[![React Native](https://img.shields.io/badge/React_Native-Mobile_App-61DAFB?style=flat-square&logo=react)](https://reactnative.dev)
[![React](https://img.shields.io/badge/React_+_Vite-Web_Platform-61DAFB?style=flat-square&logo=react)](https://react.dev)
[![Socket.IO](https://img.shields.io/badge/Socket.IO-Real--Time_Server-010101?style=flat-square&logo=socket.io)](https://socket.io)
[![Node.js](https://img.shields.io/badge/Node.js-Backend_API-339933?style=flat-square&logo=node.js)](https://nodejs.org)
[![Firebase](https://img.shields.io/badge/Firebase-Auth_%7C_FCM_%7C_Firestore-FFCA28?style=flat-square&logo=firebase&logoColor=black)](https://firebase.google.com)
[![MongoDB](https://img.shields.io/badge/MongoDB-Database-47A248?style=flat-square&logo=mongodb&logoColor=white)](https://mongodb.com)
**A 3-service full-stack platform built over 2 years — solo.**
[🌐 Live Platform](https://YOUR_LIVE_URL) · [📬 Contact Me](mailto:YOUR_EMAIL) · [💼 LinkedIn](https://linkedin.com/in/YOUR_LINKEDIN_USERNAME)
</div>
---
> [!NOTE]
> **This is a portfolio showcase repository.** It contains no source code — only documentation, architecture diagrams, and screenshots.
> The private source repositories are available for review upon request during interviews or hiring processes.
---
## 📖 The Project Story
I built this platform because I'm a live streaming enthusiast who noticed a real gap: **content creators on Indian platforms like YouTube Live had no good way to get instant on-screen alerts when viewers donated**.
Most tools were either US-centric, expensive, or required complex OBS setups that non-technical creators couldn't handle.
So I built the entire thing myself — from scratch, as a weekend and evening project over 2 years:
- A **React Native Android app** that a creator installs on their phone
- A **web dashboard** with OBS-compatible overlay widgets they can drag into their streaming software
- A **dedicated real-time server** to handle all the live events
The platform went from idea → working prototype → real users. It processes live donation events, broadcasts them to on-screen overlays within milliseconds, and handles subscription billing — all without a team.
---
## 🏗️ System Architecture
The platform is split into **three independent services** that communicate via HTTP and WebSocket:
```
┌─────────────────────────────────────────────────────────────────────┐
│                        DONATION NOTIFIER PLATFORM                    │
├─────────────────────────────────────────────────────────────────────┤
│                                                                       │
│   ┌─────────────────────┐        ┌──────────────────────────────┐   │
│   │  📱 Mobile App       │        │  🌐 Web Platform (Vercel)     │   │
│   │  DonationNotifierApp │        │  DonationAppWeb              │   │
│   │                      │        │                              │   │
│   │  React Native 0.74   │        │  React 18 + Vite (frontend) │   │
│   │  Firebase FCM        │        │  Express.js (REST API)       │   │
│   │  Notifee             │        │  MongoDB + Mongoose          │   │
│   │  Zustand             │        │  Razorpay Payments           │   │
│   │  Razorpay            │        │  OBS Overlay Widgets         │   │
│   │  RevoPush (OTA)      │        │  Firebase Admin              │   │
│   └──────────┬───────────┘        └──────────────┬───────────────┘   │
│              │                                    │                   │
│              │  Socket.IO                         │  Socket.IO        │
│              │  (events, auth)                    │  (widget updates) │
│              │                                    │                   │
│              └──────────────┬─────────────────────┘                  │
│                             │                                         │
│                   ┌─────────▼────────────┐                           │
│                   │  ⚡ Socket Server     │                           │
│                   │  DonationAppSocket   │                           │
│                   │                      │                           │
│                   │  Node.js + Socket.IO │                           │
│                   │  Firebase Auth       │                           │
│                   │  Billing Metering    │                           │
│                   │  Cricket Scraper     │                           │
│                   │  StreamElements Brdg │                           │
│                   └──────────────────────┘                           │
│                                                                       │
└─────────────────────────────────────────────────────────────────────┘
External integrations:
  Firebase (Auth · FCM · Firestore · Storage · App Check)
  MongoDB Atlas · Razorpay · Cricbuzz (scraped) · StreamElements
  Fly.io (Socket server) · Vercel (Web platform) · RevoPush (OTA)
```
---
## 📱 Repository 1 — DonationNotifierApp (React Native)
> The Android companion app installed on the creator's phone.
**What it does:**
- Listens for donation events via Socket.IO and displays rich local notifications (even with the screen off)
- Full overlay management panel — configure, preview, and switch OBS widgets from your phone
- Live statistics dashboard — today's total, top donors, donation history with date filters
- Media library for uploading custom alert sounds and overlay images
- Multi-theme support with live preview, custom sounds, and per-overlay styling
- Razorpay subscription management built in
- OTA (over-the-air) JavaScript updates via RevoPush — no Play Store re-submission
**Key technical decisions:**
- **Zustand** for global state — chosen over Redux for its minimal boilerplate in a feature-heavy app
- **Feature-based folder structure** (`src/features/`) — each feature owns its screens, hooks, and logic
- **Notifee** for notifications — gives full control over notification channels, sounds, and custom UI that FCM alone can't provide
- **Firebase App Check** to protect API endpoints from unauthorized clients
- **NativeWind** for styling — brings Tailwind's utility classes to React Native without a custom design system
**Tech stack:**
`React Native 0.74` · `Firebase (Auth, FCM, Firestore, Storage, App Check)` · `Socket.IO Client` · `Zustand` · `Notifee` · `React Navigation v6` · `Razorpay` · `RevoPush` · `NativeWind` · `Lottie`
---
## ⚡ Repository 2 — DonationAppSocket (Node.js + Socket.IO)
> The real-time event backbone — always-on, always-connected.
**What it does:**
- Receives donation events from the mobile app and broadcasts them to the creator's OBS overlay widgets in milliseconds
- Manages per-user socket rooms — events are isolated so Creator A's donation never reaches Creator B's stream
- Bridges StreamElements real-time alert events to connected clients
- Scrapes live cricket scores from Cricbuzz and pushes them to the scoreboard widget
- Meters per-session socket usage for subscription enforcement
- Firebase Admin middleware validates every single socket connection on connect
**Key technical decisions:**
- **Dedicated server** (not colocated with the web API) — because WebSocket connections are long-lived; running this on a serverless platform like Vercel would break every connection on each cold start
- **Fly.io over Render** — persistent process with no sleep time between connections; self-ping cron prevents free-tier sleep
- **Centralized state maps** (`state/connections.js`) — `connectedUsers` and `overlayConnections` Maps shared across all socket handlers without a database round-trip
- **ESM modules throughout** — consistent with the web platform; avoids CommonJS/ESM boundary issues
**Tech stack:**
`Node.js 18+ (ESM)` · `Socket.IO v4` · `Express.js` · `Firebase Admin SDK` · `Cheerio` · `node-cron` · `CryptoJS` · `Fly.io`
---
## 🌐 Repository 3 — DonationAppWeb (React + Express)
> The web platform — public site, creator dashboard, OBS widgets, and REST API.
**What it does:**
- Public marketing website with animated hero, live community counter, feature showcase, and APK download
- Protected creator dashboard: overlay manager, donation history, billing, and setup wizard
- 11 distinct OBS overlay widget types, each served at their own URL route for OBS Browser Source
- Express REST API: user auth, donation records, Razorpay order creation + webhook verification, Firebase integration, admin tools
- Admin panel for media library management and pushing live overlay updates
**Key technical decisions:**
- **Monorepo layout** (`client/` + `server/`) in one repository — simplifies Vercel deployment (one `vercel.json` handles both frontend static serving and backend serverless functions)
- **Framer Motion + React Spring** — two animation libraries used strategically; Framer for page transitions, React Spring for physics-based overlay animations
- **Vanilla CSS + CSS custom properties** — chosen deliberately over CSS-in-JS to keep overlay widgets lightweight (they run inside OBS browser sources with limited rendering resources)
- **Puppeteer with stealth plugin** — needed to bypass bot detection on web scraping targets; Cheerio alone was insufficient
- **HTTP-only cookies + JWT** — eliminates XSS token theft risk vs. `localStorage`-based auth
**Tech stack:**
`React 18` · `Vite` · `React Router v6` · `Framer Motion` · `Express.js` · `MongoDB + Mongoose` · `Firebase Admin` · `Razorpay` · `Socket.IO` · `Puppeteer` · `Cheerio` · `Helmet` · `Vercel`
---
## 🎯 What This Platform Solves
| Problem | Solution |
|---|---|
| Creator has no on-screen alert when they receive a donation | FCM push notification + Socket.IO broadcast to OBS overlay simultaneously |
| OBS overlay setup is too technical for most creators | One URL per widget, copy-paste into OBS Browser Source — done |
| Alerts need to work even when the phone screen is off | Background FCM listener via `react-native-android-notification-listener` |
| Creator app needs to stay updated without going through Play Store | RevoPush OTA for JS bundle updates, APK sideloaded via `/download` page |
| Long-lived WebSocket can't run on serverless | Dedicated Node.js server on Fly.io |
| Billing for socket usage | Per-session metering with `billing.service.js` |
---
## 📊 Project Stats
| Metric | Value |
|---|---|
| Development time | ~2 years (evenings & weekends) |
| Repositories | 3 private repos |
| Total services | 3 (Mobile, Web, Socket) |
| Overlay widget types | 11 |
| Firebase services used | 6 (Auth, FCM, Firestore, Storage, App Check, Admin SDK) |
| Platforms | Android (app) · Web (dashboard/widgets) · Node.js (API + Socket) |
---
## 📸 Screenshots
> *(Screenshots will be added here — overlay demos, dashboard view, mobile app screens)*
---
## 💼 About the Developer
**Imran Nazeer S** — Full Stack & Mobile Developer based in India.
I'm a self-taught developer who went from zero to building production-grade multi-service platforms. I specialize in **React Native**, **real-time systems (Socket.IO)**, and **full-stack JavaScript (React + Node.js)**.
This project represents 2 years of genuine interest — not a course project, not a tutorial clone. Every design decision and architecture choice above is one I researched, debated with myself, and implemented.
I'm open to **full-time roles, contract work, and freelance projects** in mobile development, full-stack web, or real-time systems.
---
### 📬 Contact & Links
| | |
|---|---|
| 📧 Email | [YOUR_EMAIL](mailto:YOUR_EMAIL) |
| 💼 LinkedIn | [linkedin.com/in/YOUR_LINKEDIN_USERNAME](https://linkedin.com/in/YOUR_LINKEDIN_USERNAME) |
| 🐙 GitHub | [github.com/YOUR_GITHUB_USERNAME](https://github.com/YOUR_GITHUB_USERNAME) |
| 🌐 Portfolio | [YOUR_PORTFOLIO_URL](https://YOUR_PORTFOLIO_URL) |
> **Recruiters / Hiring Managers**: The source code for all 3 repositories is available for review on request. I'm happy to walk through the architecture, discuss design decisions, or do a live demo on a call.
---
## 📄 License
This showcase repository is published for portfolio purposes only.  
All source code in the private repositories is **proprietary — All Rights Reserved**.
© 2024–2026 Imran Nazeer S
