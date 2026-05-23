# Donation Notifier — Android Mobile App

> A feature-rich React Native application that delivers real-time donation alerts, live stream overlay controls, and a comprehensive dashboard for content creators — all from their mobile device.

---

## 📌 Overview

**Donation Notifier** is a mobile-first companion app built for live streamers and content creators who rely on audience donations. It listens for incoming donation events through a WebSocket connection and instantly notifies the creator with rich local notifications — even when the app is in the background or the screen is off.

Beyond notifications, the app serves as a full control panel: creators can manage their stream overlays, browse donation history, configure alert sounds and themes, track real-time stats, and maintain a personal media library — all in one place.

---

## ✨ Key Features

### 🔔 Real-Time Donation Alerts
- Instant push notifications triggered via Firebase Cloud Messaging (FCM)
- Rich local notifications using **Notifee** with custom sound and vibration support
- Background notification listener (`react-native-android-notification-listener`) to capture events even when the app is closed
- In-app alert log with detailed history of all received notifications

### 🎛️ Stream Overlay Management
- Connect and configure multiple OBS/browser overlay widgets directly from the phone
- Preview and switch overlay themes on the fly
- Manage sponsor banners, top-donator lists, and challenge text overlays
- StreamElements integration for extended alert customization

### 📊 Live Statistics Dashboard
- View today's total donations, membership count, and top donors
- Historical donation breakdown with date-range filtering
- Real-time data synced via Socket.IO connection to the backend

### 🎨 Themes & Customization
- Multi-theme support with live preview before applying
- Custom alert sounds — choose from library or upload your own
- Per-overlay widget styling options

### 📚 Media Library
- Upload and organize media assets (images, sounds) for overlay use
- Document picker integration for easy file management

### 🔐 Authentication & Security
- Google Sign-In via `@react-native-google-signin/google-signin`
- Firebase Authentication with session persistence using AsyncStorage
- Firebase App Check for API request integrity
- JWT-secured API communication

### 💳 In-App Payments
- Razorpay payment gateway integration for subscription upgrades
- Membership and plan management built into the app

### 🔄 OTA Updates
- Over-the-air JavaScript bundle updates via **RevoPush / CodePush**
- In-app version check with smart update prompts
- Zero-downtime update delivery without Play Store re-submission

### 📡 Network & Connectivity
- Network state monitoring with `@react-native-community/netinfo`
- Graceful offline handling with local state caching

---

## 🛠️ Technology Stack

| Layer | Technology |
|-------|-----------|
| Framework | React Native 0.74 |
| Language | JavaScript (ES2022) |
| Navigation | React Navigation v6 (Native Stack + Bottom Tabs) |
| State Management | Zustand |
| Realtime Communication | Socket.IO Client |
| Backend Integration | Axios |
| Push Notifications | Firebase Cloud Messaging + Notifee |
| Authentication | Firebase Auth + Google Sign-In |
| Database (Remote) | Firebase Firestore |
| File Storage | Firebase Storage |
| Payments | Razorpay |
| OTA Updates | RevoPush (CodePush) |
| Styling | NativeWind (Tailwind CSS for React Native) |
| Animation | Lottie React Native |
| Media | React Native Image Picker, Video |
| Cryptography | CryptoJS |
| Date Utilities | date-fns |

---

## 📱 App Architecture

```
src/
├── app/              # Root app shell, providers, and global error boundaries
├── features/         # Feature-based modules (screens + logic co-located)
│   ├── alerts/       # Notification log and alert management
│   ├── gifts/        # Gift and donation event handling
│   ├── helpdesk/     # Support and FAQ section
│   ├── home/         # Main landing screen and quick stats
│   ├── library/      # Media asset management
│   ├── settings/     # User preferences and configuration
│   ├── stats/        # Donation statistics and analytics
│   ├── streamelements/  # StreamElements overlay integration
│   ├── themes/       # Theme selector and preview
│   └── updates/      # App version and OTA update management
├── components/       # Shared UI components
├── navigators/       # Navigation configuration and routes
├── services/         # API clients and external service adapters
├── store/            # Zustand global state stores
├── hooks/            # Reusable custom React hooks
├── helpers/          # Utility functions and formatters
├── shared/           # Shared constants, types, and configurations
└── themes/           # Design tokens, color palettes, typography
```

---

## 📸 Screenshots

> _Screenshots coming soon — see the web dashboard for overlay previews._

| Home Screen | Alerts Feed | Statistics | Settings |
|-------------|-------------|------------|----------|
| ![Home](docs/home.png) | ![Alerts](docs/alerts.png) | ![Stats](docs/stats.png) | ![Settings](docs/settings.png) |

---

## 🔗 Related Projects

This app is part of a three-repository ecosystem:

| Repository | Description |
|-----------|-------------|
| **DonationNotifierApp** ← You are here | React Native Android app for creators |
| [DonationAppWeb](../DonationAppWeb) | Web dashboard, overlay widgets, and REST API |
| [DonationAppSocket](../DonationAppSocket) | Dedicated WebSocket & real-time event server |

---

## ⚙️ Requirements

- **Android**: 8.0 (Oreo) or higher
- **Node.js**: 18 or higher (for development)
- **React Native CLI** environment (not Expo)
- Firebase project with Firestore, Auth, FCM, Storage, and App Check configured
- Active backend instances of **DonationAppWeb** and **DonationAppSocket**

---

## 📦 Installation (Development)

1. Clone the repository
2. Install dependencies with `npm install`
3. Place your `google-services.json` in the `android/app/` directory
4. Configure environment variables in a `.env` file (see `.env.example`)
5. Run on a connected Android device or emulator:
   ```
   npm run android
   ```

---

## 🚀 Distribution

The app is distributed as a signed **APK** via the companion web platform (`/download` page), allowing users to sideload the application on Android without requiring Play Store listing. OTA (over-the-air) updates are delivered via RevoPush to push JavaScript bundle changes instantly after installation.

---

## 👤 Author

**Imran Nazeer S** — Full Stack & Mobile Developer  
Built with ❤️ for the creator community.

---

## 📄 License

Private — All rights reserved.
