# How to Fix Google Sheets Access

## The Problem
You're getting a **403 Forbidden** error because:
1. The Google Sheet might not be publicly published
2. The CORS proxy is blocking access

## Solution Steps

### Step 1: Verify Google Sheet is Published
1. Open your Google Sheet
2. Go to **File → Share → Publish to web**
3. In the dropdown, select:
   - **Entire Document** (or the specific sheet)
   - **CSV** format
4. Click **Publish**
5. Copy the published link - it should look like:
   ```
   https://docs.google.com/spreadsheets/d/e/2PACX-.../pub?output=csv
   ```

### Step 2: Make Sure Sheet is Publicly Viewable
1. Click the **Share** button (top right)
2. Under "General access", select **"Anyone with the link"**
3. Set permission to **Viewer**
4. Click **Done**

### Step 3: Test the Direct Link
Open this URL in your browser (replace with YOUR link):
```
https://docs.google.com/spreadsheets/d/e/2PACX-1vRguoBxzzi0hEXpbk0hu5hivwy131-l8FRQlumD22urDW1AUiikLSAYGyZneFphJRtA0fr4vLW82na4/pub?output=csv
```

You should see CSV data directly. If you get an error page, the sheet isn't published correctly.

### Step 4: Check Your Sheet Structure
Make sure your Google Sheet has these columns (exact names don't matter, but these are recommended):

| Timestamp | Current Location | Water Level | Lat | Lng | Photo | Approved |
|-----------|------------------|-------------|-----|-----|-------|----------|
| 2026-01-16 10:30 | Vadsar | Knee deep | 22.2600 | 73.1820 | https://... | TRUE |

**Important:**
- **Lat** and **Lng** must be decimal numbers (e.g., 22.3072, not "22° 18' 26\"")
- **Approved** must be exactly: `TRUE`, `1`, or `yes` (case doesn't matter)

### Step 5: Test with the Updated Code
I've updated the code to try 4 different methods to fetch your data:
1. Direct fetch (fastest if it works)
2. AllOrigins proxy (very reliable)
3. CORS.SH proxy
4. Original CORSProxy.io

Now reload your page and check the console - it will tell you which method worked.

## Quick Test Commands

### Test 1: Can you access the sheet directly?
Open this in a new browser tab:
```
https://docs.google.com/spreadsheets/d/e/2PACX-1vRguoBxzzi0hEXpbk0hu5hivwy131-l8FRQlumD22urDW1AUiikLSAYGyZneFphJRtA0fr4vLW82na4/pub?output=csv
```

### Test 2: Run this in browser console (F12):
```javascript
fetch('https://docs.google.com/spreadsheets/d/e/2PACX-1vRguoBxzzi0hEXpbk0hu5hivwy131-l8FRQlumD22urDW1AUiikLSAYGyZneFphJRtA0fr4vLW82na4/pub?output=csv')
  .then(r => r.text())
  .then(data => console.log('Success! First 500 chars:', data.substring(0, 500)))
  .catch(err => console.error('Failed:', err));
```

If Test 1 works but Test 2 fails, it's a CORS issue (which my code now handles).

If Test 1 fails, the sheet isn't published correctly - go back to Step 1.

## What the Console Should Show (When Working)

After the fix, you should see:
```
📡 Trying: Direct fetch...
✅ Success with Direct fetch!
📄 Parsed headers: ["timestamp", "current location", "water level", "lat", "lng", "photo", "approved"]
🔍 Row 1 Debug:
   Latitude: 22.2600
   Longitude: 73.1820
   Approved field: "TRUE"
   Valid: true, Approved: true
✅ Plotted report 1: Vadsar
📊 Summary:
   Total rows: 2
   Valid coordinates: 2
   Approved: 2
   Plotted on map: 2
```
