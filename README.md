# Cynopta Android SDK Distribution

Official binary distribution repository for the **Cynopta Android SDK**.

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
    implementation 'com.github.Cynopta:android-sdk-dist:1.0.28'
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
  "license": "YOUR_CYNOPTA_LICENSE_KEY",
  "apiKey": "your-telemetry-api-key"
}
```

### Step 4: Automatic Initialization (Zero Code Changes)
The Cynopta SDK initializes automatically on app launch. You do **not** need to create or modify an `Application` class.

---

## 2. Trust Score API Usage

Query the trust score at any point in your application:

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
   implementation 'com.github.Cynopta:android-sdk-dist:1.0.28'

3. Validate that `cynopta.json` exists in `app/src/main/assets/cynopta.json` (this file should already be downloaded from the Cynopta Portal and placed there by the developer; if missing, prompt the developer to add it before proceeding).

4. Build, install, and launch the app on your emulator or device to verify integration:
   ```bash
   ./gradlew installDebug
   adb shell am start -n <YOUR_PACKAGE_NAME>/.MainActivity
   ```
   Confirm the build succeeds cleanly and the app launches without errors.
````

---

## Technical Details

- **Minimum SDK:** Android 7.0 (API Level 24)
- **Target SDK:** Android 16 (API Level 36)
- **Architectures:** `arm64-v8a`, `armeabi-v7a`, `x86`, `x86_64` (16 KB page-aligned)
- **Runtime Permissions:** None required
- **License:** Proprietary. Contact Cynopta for enterprise licensing.
