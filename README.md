# ⚡ PlanFlow — Personal Daily Planner

> A fully customizable daily planner with real-time cloud sync, custom categories, and Google Sign-In. Built as a production-ready single-file web app — deployable to GitHub Pages in minutes.

![PlanFlow Preview](https://img.shields.io/badge/status-production--ready-brightgreen)
![Firebase](https://img.shields.io/badge/backend-Firebase-orange)
![License](https://img.shields.io/badge/license-MIT-blue)

---

## ✨ Features

- **Custom Categories** — Create unlimited categories with custom name, description, color, and emoji icon. Finance, AI/ML, Health, Deep Work, Learning — anything you need.
- **Google Sign-In** — Secure authentication. Only you can access your data.
- **Real-Time Cloud Sync** — Changes sync instantly across laptop, phone, and tablet via Firebase Firestore.
- **Weekly Timeline** — Visual hourly timeline from 5am to midnight with current-hour highlighting.
- **List View** — Clean compact list alternative to the timeline.
- **Priority Levels** — High 🔴 / Medium 🟡 / Low ⚪ per task.
- **Task Notes** — Optional notes on every activity.
- **Progress Tracking** — Daily stats: total tasks, completed, hours planned, top category.
- **Motivational Quotes** — Rotating productivity quotes with refresh button.
- **Export Data** — One-click JSON export of all tasks and categories.
- **No tracking, no ads** — Your data stays in your Firebase project.

---

## 🚀 Getting Started

### 1. Clone or download

```bash
git clone https://github.com/YOUR_USERNAME/planflow.git
cd planflow
```

### 2. Create a Firebase project

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Click **Add project** → name it `planflow` → Continue
3. Disable Google Analytics if you don't need it → **Create project**

### 3. Enable Google Sign-In

1. In the Firebase Console → **Build → Authentication**
2. Click **Get started** → **Sign-in providers**
3. Enable **Google** → add your email as support email → **Save**

### 4. Create Firestore Database

1. **Build → Firestore Database → Create database**
2. Choose **Start in test mode** → select a region → **Done**
3. Go to the **Rules** tab, replace the content with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    // User profiles
    match /users/{userId} {
      allow read, write: if request.auth.uid == userId;

      // Categories subcollection
      match /categories/{catId} {
        allow read, write: if request.auth.uid == userId;
      }
    }

    // Tasks
    match /tasks/{taskId} {
      allow read, update, delete: if request.auth.uid == resource.data.uid;
      allow create: if request.auth != null;
    }
  }
}
```

Click **Publish**.

### 5. Get your Firebase config

1. Click the **gear icon ⚙️** → **Project settings**
2. Scroll to **Your apps** → click the **`</>`** web icon
3. Register the app (any name) → copy the `firebaseConfig` object

### 6. Paste your config into index.html

Open `index.html` in any text editor. Find this section near the top:

```javascript
const firebaseConfig = {
  apiKey:            "PASTE_YOUR_apiKey_HERE",
  authDomain:        "PASTE_YOUR_authDomain_HERE",
  projectId:         "PASTE_YOUR_projectId_HERE",
  ...
};
```

Replace with your actual config values.

### 7. Deploy to GitHub Pages

1. Push your repo to GitHub
2. Go to **Settings → Pages**
3. Source: **Deploy from branch → main → / (root)** → Save
4. Your app is live at: `https://YOUR_USERNAME.github.io/planflow`

---

## 📱 Add to iPhone Home Screen

1. Open your GitHub Pages URL in **Safari**
2. Tap the **Share** button (box with arrow)
3. Tap **"Add to Home Screen"**
4. It behaves like a native app — no App Store needed.

---

## 🗂️ Project Structure

```
planflow/
├── index.html      # The entire app — HTML, CSS, JS in one file
└── README.md       # This file
```

Single-file architecture means zero build steps, zero dependencies, and instant deployment.

---

## 🛠️ Customization Guide

### Changing default quotes
Find the `QUOTES` array in the JavaScript section and add your own lines:
```javascript
const QUOTES = [
  '"Your quote here." — Author',
  ...
];
```

### Changing the color palette for categories
Find the `PALETTE` array:
```javascript
const PALETTE = ['#6ee7b7', '#60a5fa', ...];
```

### Changing the app name / branding
Search for `PlanFlow` in the file and replace with your brand name.

---

## 💰 Selling / Licensing

This project is released under the **MIT License** — you are free to:
- Use it for personal or commercial projects
- Sell it as a template or SaaS product
- Modify and rebrand it

If you sell it, consider:
- Adding a custom domain (e.g. via Namecheap or Google Domains → link to GitHub Pages)
- Setting up [Firebase pricing](https://firebase.google.com/pricing) — the free Spark plan supports ~50,000 reads/day which covers hundreds of users
- Adding Stripe for payments if building a multi-tenant SaaS version

---

## 📋 Firebase Free Tier Limits (Spark Plan)

| Resource | Free Limit |
|----------|-----------|
| Firestore reads | 50,000/day |
| Firestore writes | 20,000/day |
| Auth users | Unlimited |
| Hosting | 10 GB/month |

More than enough for personal use and small commercial projects.

---

## 📄 License

MIT © 2025 — Free to use, modify, and sell.
