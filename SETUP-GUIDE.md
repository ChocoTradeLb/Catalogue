# Wholesale Hub — App Setup Guide

Your website is now a **PWA (Progressive Web App)**. That means customers can
**install it on their phone like a real app** (icon on the home screen, opens
fullscreen) and you can **send them push notifications** (new arrivals, offers).

This guide has 3 parts:
1. Put the files on GitHub (you already do this)
2. Turn on push notifications (OneSignal — free, manual "type & send")
3. (Optional, later) Make a real Android APK for the Play Store

---

## 1. Files to upload to GitHub

Upload ALL of these to your GitHub Pages repo (keep the folder structure):

```
index.html
products.csv
manifest.json
service-worker.js
icons/
  icon-192.png
  icon-512.png
  icon-maskable-512.png
  apple-touch-icon.png
  favicon-48.png
```

> ⚠️ The app MUST be served over **https** for install + notifications to work.
> GitHub Pages already uses https, so you're fine.

Once uploaded, open your GitHub Pages URL on a phone. In Chrome (Android) you'll
get an "Install app" prompt, and the **⬇️ Install App** button appears in the header.
On iPhone (Safari): tap **Share → Add to Home Screen**.

---

## 2. Turn on push notifications (OneSignal — free & manual)

OneSignal gives you a **dashboard where you type a message and click Send** — no
coding needed to send notifications. Free for your size of audience.

### One-time setup (about 10 minutes)

1. Go to **https://onesignal.com** and create a free account.
2. Click **New App/Website** → name it "Wholesale Hub".
3. Choose **Web** as the platform.
4. Under "Choose Integration" pick **Custom Code** (also called "Typical Site").
5. It will ask for your **Site URL** → paste your GitHub Pages URL
   (e.g. `https://yourname.github.io/yourrepo/`).
6. It will show you an **App ID** (a long code like `abc12345-...`).
   **Copy it.**
7. Open `index.html`, find this line near the top:

   ```js
   appId: "YOUR_ONESIGNAL_APP_ID",
   ```

   Replace `YOUR_ONESIGNAL_APP_ID` with the App ID you copied. Save & re-upload
   `index.html` to GitHub.

8. OneSignal also gives you two files: **`OneSignalSDKWorker.js`** (and sometimes
   asks about a service worker path). Download it and upload it to the SAME folder
   as `index.html` on GitHub. (If OneSignal asks for the "service worker scope/path",
   leave it as the default root.)

That's it. Now visitors will see the **🔔 Enable Alerts** button in your app; when
they tap it and allow, they're subscribed.

### Sending an offer / new-arrival notification

1. Log into OneSignal → your app → **Messages → New Push**.
2. Type your title (e.g. "🔥 New Arrivals!") and message
   (e.g. "Fresh stock of Kinder & Nutella just landed. Tap to order!").
3. (Optional) Add a **Launch URL** = your app URL so tapping opens the catalog.
4. Click **Review & Send**. Done — everyone who enabled alerts gets it.

> 📱 **Android:** notifications work great once installed or even in the browser.
> 🍎 **iPhone:** the customer must first **Add to Home Screen** (install it), and be
> on iOS 16.4+. After that, notifications work. This is an Apple limitation, not a
> bug in your app.

---

## 3. (Optional, later) Make a real Android APK for the Play Store

Because it's already a PWA, you can wrap it into a Play-Store Android app with
almost no extra work using **PWABuilder** (free, made by Microsoft):

1. Go to **https://www.pwabuilder.com**
2. Paste your GitHub Pages URL and click **Start**.
3. It scores your PWA and lets you **download an Android package (APK/AAB)**.
4. Follow its steps to sign the app and upload to the Google Play Console
   (one-time $25 Google developer fee).

The APK version will use the same notifications you set up in step 2.

For iPhone/App Store you'd need a Mac + Apple Developer account ($99/yr);
most wholesale businesses skip this and rely on the "Add to Home Screen" PWA on
iPhone, which is free.

---

## Quick recap of what to do next

- [ ] Upload all files (incl. `manifest.json`, `service-worker.js`, `icons/`) to GitHub
- [ ] Create OneSignal account, get App ID, paste it into `index.html`, re-upload
- [ ] Upload OneSignal's `OneSignalSDKWorker.js` to your repo
- [ ] Test: open the URL on your phone, tap **Install App**, then **Enable Alerts**
- [ ] Send yourself a test notification from the OneSignal dashboard
- [ ] (Later) Use PWABuilder to make the Play Store APK

Need help with any step? Just ask.
