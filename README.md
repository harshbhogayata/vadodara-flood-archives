# Vadodara Files 📂
*(Formerly Vadodara Flood Archives)*

A verified digital archive of flood risk in Vadodara (2019-2025) and a live relief coordination system ("SewaSetu").

![Preview](social-preview.png)

## What is this?

**1. The Archive (Vadodara Files)**
A map of 50+ locations in Vadodara with their flood history. Each zone has a risk score based on satellite data, news reports, and VMC bulletins. 
- **Red Zones**: Critical risk (Water > Waist deep).
- **Yellow Zones**: Moderate risk (Waterlogging).
- **Green Zones**: Safe history.

**2. The Relief System (SewaSetu)**
A built-in mode for active emergency response.
- **Find Shelters**: Locate verified safe houses/schools.
- **Community Reports**: Crowdsourced live flood updates.
- **Live SOS Feed**: Real-time needs (Food, Rescue, Meds).

## Features

- **Risk Simulator**: Interactive flood modeling (Ajwa Dam levels + Rainfall).
- **Android Ready**: Runs as a native app via WebView (see below).
- **Offline Capable**: Critical data works with spotty internet.
- **Privacy First**: Zero tracking, local-first architecture.

## How to use

1.  **Check your area**: Use the search bar in "Analysis" tab.
2.  **Verify Risk**: Click any zone to see year-by-year flood history.
3.  **Emergency Mode**: Toggle the siren icon (🚨) to switch to SewaSetu mode.

---

## 📱 Android Integration

This project is optimized to run as a native Android app.

**1. Setup in Android Studio**
- Create a new "Empty Activity" project.
- Create an `assets` folder in `app/src/main/`.
- Copy ALL files from this repo (`index.html`, `style.css`, `app.js`, `manifest.json`, etc.) into `assets/`.

**2. WebView Code (Kotlin)**
Add this to your `MainActivity.kt`:

```kotlin
myWebView.settings.apply {
    javaScriptEnabled = true
    domStorageEnabled = true
    databaseEnabled = true
    allowFileAccess = true
    geolocationEnabled = true // Required for "Am I Safe?"
}
myWebView.loadUrl("file:///android_asset/index.html")
```

**3. Build & Install**
Run `./gradlew installDebug` to install on your connected phone.

---

## Technical Details

- **Stack**: HTML5, CSS3 (Glassmorphism), Vanilla JS.
- **Map Engine**: Leaflet.js + OpenStreetMap.
- **Data**: Static JSON (Verified by Civic Tech Initiative).

## Contributions

If you have verified photos or data for a specific area in Vadodara, please open a PR or Issue. Accuracy is our top priority.

*Powered by Vadodara Files Initiative.*
