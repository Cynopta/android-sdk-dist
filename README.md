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
    implementation 'com.github.Cynopta:android-sdk-dist:1.0.15'
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

### Step 4: Initialize in Application.onCreate
```kotlin
package com.example.myapp

import android.app.Application
import com.cynopta.sdk.Cynopta

class MyApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        Cynopta.start(this)
    }
}
```

---

## 2. Automatic Integration with AI Agents (Cursor, Antigravity, Copilot, Claude)

Copy and paste this prompt directly into your AI coding assistant:

```markdown
Integrate the Cynopta Android SDK into this project:

1. Add JitPack repository into settings.gradle or settings.gradle.kts:
   maven { url 'https://jitpack.io' }

2. Add dependency to app/build.gradle:
   implementation 'com.github.Cynopta:android-sdk-dist:1.0.15'

3. Create app/src/main/assets/cynopta.json with:
   {
     "license": "<YOUR_LICENSE_TOKEN>",
     "apiKey": "<YOUR_API_KEY>"
   }

4. In the Application class onCreate() method, add:
   Cynopta.start(this);

5. Run ./gradlew assembleDebug to verify compilation.
```

---

## Technical Details

- **Minimum SDK:** Android 7.0 (API Level 24)
- **Target SDK:** Android 16 (API Level 36)
- **Architectures:** `arm64-v8a`, `armeabi-v7a`, `x86`, `x86_64` (16 KB page-aligned)
- **Runtime Permissions:** None required
- **License:** Proprietary. Contact Cynopta for enterprise licensing.
