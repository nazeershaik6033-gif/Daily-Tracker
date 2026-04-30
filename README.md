# Expense Tracker Pro — PWA

A self-contained Progressive Web App. Drop the folder on any HTTPS host, then
"Add to Home Screen" from iPhone Safari to install it like a native app.

All data lives in your phone's localStorage — nothing is sent anywhere.

---

## 1. Files in this folder

```
expense-tracker-pwa/
├── index.html              ← the entire app (single file, ~85 KB)
├── manifest.json           ← PWA metadata (name, icons, theme)
├── icon-180.png            ← iOS Add-to-Home-Screen icon
├── icon-192.png            ← Android / Chrome
├── icon-512.png            ← Android / Chrome
└── icon-512-maskable.png   ← Android adaptive icon
```

You don't need a build step. It's already built. Just host these files.

---

## 2. Get it online (the 5-minute path)

The fastest free option is **Netlify Drop** — no account needed for a quick
preview, and a free account gets you a permanent URL.

1. Open <https://app.netlify.com/drop> on a desktop browser.
2. Drag the **whole folder** (not the zip) onto the page.
3. Wait ~5 seconds. You'll get a URL like `dancing-walrus-abc123.netlify.app`.
4. (Optional) Sign in to claim the site so the URL doesn't expire.

That's it. The URL works on any device.

### Other free hosts that work

| Host                | Setup                                                     |
| ------------------- | --------------------------------------------------------- |
| Cloudflare Pages    | Sign in → "Upload assets" → drag the folder               |
| Vercel              | `npx vercel` from the folder (requires Node)              |
| GitHub Pages        | Push folder to a repo, enable Pages in Settings           |
| Surge.sh            | `npm i -g surge && surge` from the folder                 |
| Your own web server | Upload via FTP/SSH — any HTTPS static host works          |

**Important:** the host must serve over **HTTPS**. Plain `http://` won't fully
install on iOS.

---

## 3. Install on iPhone

1. Open the URL in **Safari** (not Chrome — Chrome can't add to home screen on iOS).
2. Tap the **Share** button (square with up-arrow).
3. Scroll down → tap **Add to Home Screen**.
4. Tap **Add** in the top-right.

The app appears on your home screen with the lime "$" icon. Tap it — it
launches full-screen with no browser UI, just like a native app.

---

## 4. What works, what doesn't

### Works on iPhone

- All the in-app features: dashboard, calendar, recurring expenses, transfers,
  search, calculator, profiles, accounts, multi-currency, JSON backup/restore.
- Full-screen launch with status bar handled correctly.
- Notch and home-indicator safe-area padding.
- Data persists across app launches (in localStorage).
- Works offline after the first online launch (browser caches CDN scripts).

### Doesn't work in a PWA

- **Reading SMS automatically.** Browsers can't read SMS. The "Smart Paste" tab
  works — you copy a bank SMS and paste it.
- **Push notifications and Home-Screen widgets.** iOS limits PWA capabilities
  here. App-Store apps via Capacitor can do these.
- **iCloud sync, Apple Pay Shortcuts, Face ID lock.** All native-only.
- The app **isn't searchable in the App Store.** It only lives on the home
  screen of devices that installed it from your URL.

---

## 5. Backup your data

Settings → Backup & Restore → **Copy** to clipboard.

Paste the JSON anywhere safe (Notes, email yourself, save to Files). To
restore on another phone, install the PWA the same way and paste the JSON
into the Restore box.

> Note: iOS Safari may evict localStorage data after ~7 days of no app use.
> Once installed on the home screen and opened regularly, this rarely
> triggers, but a periodic Backup is the safe move.

---

## 6. Updating the app later

If you make changes to `ExpenseTrackerPro.jsx` and rebuild, just re-upload
`index.html` to your host. Open the home-screen icon — iOS will fetch the new
version on the next online launch. (To force-refresh sooner, delete and
re-add the home-screen icon.)

---

## 7. If you change your mind and want App Store

Coming back to this chat and asking for the Capacitor path will produce a
full Xcode project from this same code. You'd need a Mac, an Apple Developer
account ($99/yr), and patience for App Store review.
