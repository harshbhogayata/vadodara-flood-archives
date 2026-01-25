# Vadodara Flood Archives

This started because I watched the 2024 monsoon unfold on Twitter. Vadsar was underwater. Sayajigunj roads became rivers. People were posting videos asking "is my area safe?" — but there was no single place to check.

So I built one.

## What this is

A map of 50+ locations in Vadodara with their flood history from 2019-2025. Each zone has a risk score calculated from actual events — not predictions, not models, just what happened.

The score works like this:
- 2024 and 2025 data gets the most weight (35 points each)
- 2019 gets 20 points (historic benchmark)
- "Waist deep" or "evacuated" = full points
- "Waterlogged" or "knee deep" = half points
- "Safe" = zero

Red zones scored 70+. Yellow zones scored 15-40. You get the idea.

## Features

- **Risk Simulator** — Slide the Ajwa Dam level and rainfall to see what happens
- **Zone Search** — Find any area instantly in the Analysis tab
- **Click to Fly** — Click a zone card, map takes you there
- **Gujarati Support** — Click ગુ to switch languages
- **Mobile Ready** — Works on phones with a bottom sheet UI

## The river

The Vishwamitri runs through the middle of Vadodara. When it floods, everything within 500 meters goes first. The blue line on the map shows the general path. Notice how the red dots cluster around it.

## Data sources

- ISRO Bhuvan satellite imagery
- VMC official bulletins
- News reports (TOI, DeshGujarat, ABP)

I manually verified each entry. If a zone is marked "Waist Deep 2024", there's a news article or satellite image to back it up.

## Disclaimer

This is a research archive, not an official warning system. Past flooding doesn't guarantee future risk. Don't use this to make property decisions. For actual emergencies, contact VMC directly.

## Made with

Plain HTML, CSS, JavaScript, and Leaflet.js. No frameworks. Runs on any static host.

---


---

# Android Integration 📱

This project is now optimized to run as a native Android app using WebView.

## 1. Setup in Android Studio

1.  **Create New Project**: Select "Empty Activity" or "No Activity".
2.  **Create Assets Folder**:
    *   Right-click `app/src/main` -> New -> **Directory**.
    *   Name it `assets`.
3.  **Copy Files**:
    *   Copy ALL files from this folder (`index.html`, `style.css`, `app.js`, `manifest.json`, etc.) into `app/src/main/assets/`.

## 2. WebView Code (Kotlin)

Paste this into your `MainActivity.kt`:

```kotlin
// MainActivity.kt
import android.webkit.WebView
import android.webkit.WebViewClient

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val myWebView: WebView = findViewById(R.id.webview)
        
        myWebView.settings.apply {
            javaScriptEnabled = true
            domStorageEnabled = true
            databaseEnabled = true
            allowFileAccess = true
            geolocationEnabled = true
        }

        myWebView.webViewClient = WebViewClient()
        myWebView.loadUrl("file:///android_asset/index.html")
    }
}
```

## 3. Permissions (AndroidManifest.xml)

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

