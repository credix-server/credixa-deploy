# 🔥 Credixa Cloud Sync — Firebase Setup Guide

## Why this is needed
`localStorage` only exists on **one device/browser**. To see user data on your admin panel,
you need a real cloud database. Firebase Firestore is **free** for your usage level.

---

## Step 1 — Create Firebase Project (5 minutes)

1. Go to **https://console.firebase.google.com**
2. Click **"Add project"** → Name it `credixa` → Continue → Create project
3. In the left sidebar, click **"Firestore Database"**
4. Click **"Create database"** → Choose **"Start in test mode"** → Select a region → Enable

---

## Step 2 — Get Your Config Keys

1. In Firebase Console, click the ⚙️ gear icon → **"Project settings"**
2. Scroll down to **"Your apps"** → Click **"</> Web"**
3. Register app name: `credixa` → Click **"Register app"**
4. You'll see a config block like this:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "credixa-xxxxx.firebaseapp.com",
  projectId: "credixa-xxxxx",
  storageBucket: "credixa-xxxxx.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

---

## Step 3 — Update Both HTML Files

Open **both** `admin.html` and `index.html` in a text editor (Notepad is fine).

Find this section near the top of each file (in the `<script type="module">` block):

```javascript
const FIREBASE_CONFIG = {
  apiKey: "REPLACE_WITH_YOUR_API_KEY",
  authDomain: "REPLACE_WITH_YOUR_PROJECT.firebaseapp.com",
  projectId: "REPLACE_WITH_YOUR_PROJECT_ID",
  ...
};
```

Replace **all 6 REPLACE_WITH_... values** with your actual values from Step 2.

Do this in **both files** — they must have the same config.

---

## Step 4 — Set Firestore Rules (allow access)

1. In Firebase Console → Firestore → **"Rules"** tab
2. Replace the rules with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

3. Click **Publish**

> ⚠️ These are open rules — fine for a private app. For extra security later,
> you can add authentication.

---

## Step 5 — Re-deploy to Netlify

Upload the updated `admin.html` and `index.html` to your GitHub repo and Netlify will auto-deploy.

---

## How It Works After Setup

| Action | Result |
|--------|--------|
| User adds a client on their phone | Instantly saved to cloud |
| You open admin.html | Pulls latest data from cloud |
| Admin creates/edits a user | User's app sees changes on next refresh |
| Real-time: admin panel open while user adds data | Admin panel updates automatically |

---

## ❓ Troubleshooting

- **"REPLACE_WITH_..." still in file** → You forgot to edit the config values
- **Data not syncing** → Check browser console (F12) for Firebase errors
- **"Permission denied"** → Redo Step 4 (Firestore rules)
- **Free tier limits** → Firebase free tier allows 50,000 reads/day and 20,000 writes/day — more than enough

---

## 💡 Important Notes

- The **first time** you deploy with Firebase, all existing localStorage data stays local.
  To migrate: go to admin.html → Settings → Export Backup → then Import Backup (this pushes it to cloud)
- Users must be **online** for data to sync. Offline changes sync when they reconnect.
