## 📌 Overview  
**Donation Notifier** is a full-stack system for streamers and content creators.  
It integrates **Firebase authentication, subscription management, real-time payment alerts, and overlays** for live streams.  

The system consists of:  
- 📱 **React Native Mobile App** – alert listener & subscription validation  
- 🌐 **React.js Web App** – admin panel for managing users & subscriptions  
- ⚡ **Socket.IO Backend** – real-time communication for alerts & overlays  

---

## ✨ Features  

### 📱 Mobile App (React Native)  
- Google login with Firebase  
- Start/Stop listening for alerts  
- Real-time alert push to overlays  
- Subscription validation 
- Push notification support (RevoPush)  

### 🌐 Web App (React.js)  
- Admin panel for users & subscriptions  
- Search users by email  
- Assign subscription (1 / 2 / 3 months)  
- Firebase authentication (admin-only)  
- Email verification for PhonePe alerts  

### ⚡ Backend (Socket.IO + Express)  
- Real-time donation alerts for overlays  
- Secure API for pushing events  
- Auto-disconnect & keep-alive pings  
- Firebase Admin SDK integration  

---

## 🛠️ Tech Stack  
- **Frontend (Web):** React.js, Tailwind CSS, Firebase  
- **Mobile:** React Native CLI, Firebase Auth, RevoPush  
- **Backend:** Node.js, Express.js, Socket.IO  
- **Database:** Firestore  
- **Hosting:** Vercel (Web), Render (Backend)

- REACT NATIVE APP SCREENSHOT

<img width="250" height="541" alt="Home" src="https://github.com/user-attachments/assets/70986aa2-df00-4e7d-ba38-0f973199aab1" />
<img width="250" height="541" alt="History" src="https://github.com/user-attachments/assets/03160834-ad1a-411e-80c8-88dab203e331" />
