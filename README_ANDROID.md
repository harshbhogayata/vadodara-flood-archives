# Vadodara Files - Android Studio Integration Guide

## Overview
This project is a static web application (HTML/CSS/JS) designed to run perfectly inside an Android WebView.

## 1. Setup in Android Studio

1.  **Create New Project**: Select "Empty Activity" or "No Activity".
2.  **Create Assets Folder**:
    *   Right-click `app/src/main` -> New -> **Directory**.
    *   Name it `assets`.
3.  **Copy Files**:
    *   Copy ALL files from this folder (`index.html`, `style.css`, `app.js`, `data.js`, `manifest.json`, etc.) into `app/src/main/assets/`.

## 2. WebView Implementation (MainActivity.java/kt)

Use the following configuration to ensure features like Geolocation and File Access work:

```kotlin
// MainActivity.kt
import android.webkit.WebView
import android.webkit.WebViewClient
import android.webkit.WebSettings

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val myWebView: WebView = findViewById(R.id.webview)
        
        // Critical Settings for Vadodara Files
        myWebView.settings.apply {
            javaScriptEnabled = true
            domStorageEnabled = true // For LocalStorage/Session
            databaseEnabled = true
            allowFileAccess = true
            useWideViewPort = true
            loadWithOverviewMode = true
            geolocationEnabled = true // For "Am I Safe" feature
        }

        // Handle navigation inside the app
        myWebView.webViewClient = WebViewClient()

        // Load the local index.html
        myWebView.loadUrl("file:///android_asset/index.html")
    }
}
```

## 3. Permissions (AndroidManifest.xml)

Add these permissions for full functionality (Live Feed & Maps):

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<!-- If using local file loading heavily -->
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

## 4. Troubleshooting
*   **Maps not loading?** Ensure `INTERNET` permission is granted.
*   **Location failed?** You must request runtime location permissions in full Android code (Java/Kotlin) before the WebView can use `navigator.geolocation`.
*   **CORS Errors?** The Community Reports feature uses external APIs. IF it fails in WebView, add `android:usesCleartextTraffic="true"` to your `<application>` tag in Manifest.

## Integration Note
*   **SewaSetu Integration**: The "Relief Mode" is powered by SewaSetu logic. This is embedded directly in `app.js`.

## 5. Building & Installing (Debug Commands)

Once your project is set up in Android Studio, here is how to get the debug app onto your phone:

### Option A: From Android Studio (Easiest)
1.  Connect your Android phone via USB.
2.  Enable **USB Debugging** on your phone (Settings -> Developer Options).
3.  Click the Green **Run** button (▶️) in the top toolbar of Android Studio.

### Option B: Command Line (advanced)
Open the "Terminal" tab at the bottom of Android Studio and run:

**Windows:**
```powershell
./gradlew installDebug
```

**Mac/Linux:**
```bash
./gradlew installDebug
```

### Option C: Manual APK Transfer
1.  Build the APK: `Build -> Build Bundle(s) / APK(s) -> Build APK(s)`.
2.  Locate the file: usually in `app/build/outputs/apk/debug/app-debug.apk`.
3.  Transfer this file to your phone via USB or WhatsApp and install it.
