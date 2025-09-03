🎉 Donation Notifier – React Native + React.js Web + Socket.IO

📌 Overview

Donation Notifier is a complete system built with React Native (mobile app), React.js (web app), and Socket.IO (backend).
It integrates Firebase authentication, subscription management, real-time payment alerts, and streaming overlays.

The system is designed for streamers and content creators to:

Receive donation/payment notifications (GPay, Paytm, PhonePe).

Manage subscriptions via a secure admin panel.

Push real-time alerts to StreamElements / Streamlabs overlays.

✨ Key Features
📱 React Native Mobile App

Google login with Firebase.

Start/Stop listening for payment notifications.

Real-time donation alerts pushed to overlays.

Subscription validation inside the app.

Push notification support (RevoPush).

🌐 React.js Web App

Admin panel for managing users & subscriptions.

Search users by email and assign subscription plans (1 / 2 / 3 months).

Firebase-secured authentication (admin-only access).

Email verification for forwarding PhonePe alerts.

⚡ Socket.IO Backend

Real-time overlay communication for live alerts.

Secure API for pushing donation events.

Auto-disconnect & keep-alive ping every 10 minutes.

Built with Node.js + Express + Firebase Admin SDK.

🛠️ Tech Stack

Frontend (Web): React.js, Tailwind CSS, Firebase

Mobile: React Native (CLI), Firebase Auth, RevoPush

Backend: Node.js, Express.js, Socket.IO, Firebase Admin SDK

Database: Firestore

Hosting: Vercel (Web), Render (Backend)

📸 Screenshots
Mobile App	Web Dashboard	Overlay Alerts

	
	

(Replace with your actual screenshots to showcase your project.)

🔗 Demo Links

📱 Mobile App (APK): Download Here

🌐 Web App: Visit Here

🖥️ Overlay Link: Overlay URL

🧪 Demo Workflow

User logs in via Google (mobile app).

User enables Start Listening → app begins fetching donation/payment alerts.

Alerts are sent to the backend → Socket.IO → Stream overlay → Displayed on stream.

Admin (via web app) can update/extend subscriptions securely.

🎯 Project Highlights

End-to-end system combining mobile, web, and backend.

Secure Firebase authentication for users and admins.

Real-time donation alerts for stream overlays.

Subscription & payment validation integrated into workflow.

📜 License

This project is for demo and showcase purposes only.
Source code is private, but architecture and workflow details are shared here for evaluation.
