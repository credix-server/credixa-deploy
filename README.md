# CREDIXA — Deployment Guide

## Files in This Package
```
index.html          ← USER APP (convert to APK, share with clients)
admin.html          ← ADMIN CMS (use on your PC only)
manifest.json       ← PWA manifest for APK conversion
service-worker.js   ← Offline support
_redirects          ← Netlify routing rules
netlify.toml        ← Netlify build & header config
Gemini_Generated_Image_l3cvtwl3cvtwl3cv.png  ← App icon (app icon)
Gemini_Generated_Image_1s696g1s696g1s69.png  ← Logo image
```

## LOGIN CREDENTIALS

### Admin CMS (admin.html)
- **Username:** `admin`
- **PIN:** `87654321`

### Demo User (index.html)  
- **PIN:** `123456` (auto-created on first admin login)

## DEPLOYMENT STEPS

### 1. Upload to GitHub
- Go to https://github.com → New repository → `credixa-deploy`
- Upload ALL files in this folder

### 2. Deploy to Netlify
- Go to https://app.netlify.com
- Click "Add new site" → "Import an existing project"
- Connect to GitHub → Select `credixa-deploy`
- Build settings: leave empty (publish directory: `.`)
- Click "Deploy site"

### 3. Your URLs
```
USER APP (→ APK):  https://YOUR-SITE.netlify.app
ADMIN CMS:         https://YOUR-SITE.netlify.app/admin.html
```

### 4. Convert to APK
1. Go to https://www.pwabuilder.com
2. Enter: `https://YOUR-SITE.netlify.app`
3. Click Start → Package for Stores → Android
4. App name: Credixa | Package: com.credixa.app
5. Download → Share via WhatsApp

## HOW ADMIN→USER SYNC WORKS
Both admin.html and index.html share the same `localStorage` key (`credixa_v2`).
- Admin makes changes → changes are live immediately
- Users need to **refresh their app** (pull down to refresh or tap "Aktualisa Datos" in Profile)
- When hosted on Netlify, changes made in admin are reflected in user app on same device/browser
- For cross-device sync: use the "Export Backup" / "Import Backup" feature in Settings

## WORKFLOW
1. Client requests access → sends you their info
2. You open admin.html → Create New User → fill details + photo + 6-digit PIN
3. Send client: APK + their PIN
4. Client installs, enters PIN, sees their photo, confirms, enters app
5. Client manages their lottery credit business from their phone
