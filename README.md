# Cynopta Android SDK Distribution

Official binary distribution repository for the **Cynopta Security & Trust Android SDK**.

---

## 1. Quick Integration

### Step 1: Add JitPack to Repositories
Add JitPack to your project's `settings.gradle` (or root `build.gradle`):

```groovy
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}
```

*(Or in Kotlin DSL `settings.gradle.kts`):*
```kotlin
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven(url = "https://jitpack.io")
    }
}
```

### Step 2: Add Dependency
Add the Cynopta SDK to your app module's `build.gradle` (or `build.gradle.kts`):

```groovy
dependencies {
    implementation 'com.github.Cynopta:android-sdk-dist:1.0.16'
}
```

### Step 3: Add License & Configuration (`cynopta.json`)
Obtain your `cynopta.json` file from the Cynopta Portal and place it in your application module's `assets/` directory:
```
app/src/main/assets/cynopta.json
```

Example `cynopta.json`:
```json
{
  "license": "eyJjZXJ0cyI6W10sImV4cCI6MTgyMjU3OTg4OCwicGtnIjoiY29tLmN5bm9wdGEuZGVtbyIsInZlciI6MX0...",
  "apiKey": "your-telemetry-api-key"
}
```

### Step 4: That's It! (Zero Code Changes)
The Cynopta SDK automatically initializes on app launch using **AndroidX App Startup**. You do **not** need to create or modify an `Application` class.

---

## 2. Trust Score API Usage

Query the continuous trust score at any point in your application:

### Asynchronous (Main / UI Thread)
```kotlin
import com.cynopta.sdk.Cynopta
import com.cynopta.sdk.TrustCallback
import com.cynopta.sdk.TrustEvaluation

Cynopta.getLatestTrustEvaluation(context, object : TrustCallback {
    override fun onResult(evaluation: TrustEvaluation) {
        val score: Float = evaluation.score // 0.00 (Untrusted) to 1.00 (Verified Human)
        // Apply your application logic based on the trust score
    }

    override fun onError(error: Throwable) {
        // Handle evaluation failure
    }
})
```

### Synchronous (Background Thread / Coroutines)
```kotlin
val evaluation = Cynopta.getLatestTrustEvaluation(context)
val score: Float = evaluation.score
```

---

## 3. Automatic Integration with AI Agents (Cursor, Antigravity, Copilot, Claude)

Copy and paste this prompt directly into your AI coding assistant:

````markdown
Integrate the Cynopta Android SDK into this project:

1. Add JitPack repository into settings.gradle or settings.gradle.kts:
   maven { url 'https://jitpack.io' }

2. Add dependency to app/build.gradle:
   implementation 'com.github.Cynopta:android-sdk-dist:1.0.16'

3. Validate that `cynopta.json` exists in `app/src/main/assets/cynopta.json` (this file should already be downloaded from the Cynopta Portal and placed there by the developer; if missing, prompt the developer to add it before proceeding).

4. Install, Launch & Verify via ADB:
   Install the APK on your running emulator/device, launch it, and assert the Logcat success marker:
   ```bash
   ./gradlew installDebug
   adb shell am start -n <YOUR_PACKAGE_NAME>/.MainActivity
   sleep 3
   adb logcat -d -s CynoptaSDK | grep "Cynopta SDK initialized successfully"
   ```
   Confirm that Logcat outputs `Cynopta SDK initialized successfully`.
   (The SDK auto-starts on app launch via AndroidX App Startup; zero Kotlin/Java code changes are required).
````

---

## Technical Details

- **Minimum SDK:** Android 7.0 (API Level 24)
- **Target SDK:** Android 16 (API Level 36)
- **Architectures:** `arm64-v8a`, `armeabi-v7a`, `x86`, `x86_64` (16 KB page-aligned)
- **Runtime Permissions:** None required
- **License:** Proprietary. Contact Cynopta for enterprise licensing.
