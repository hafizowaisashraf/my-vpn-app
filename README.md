# SecureShield VPN for Android

SecureShield VPN is a modern, production-ready Android VPN client engineered with **Kotlin**, **Jetpack Compose (Material 3)**, and Android's native **VpnService** API.

---

## 🛡️ Core Highlights

1. **Android VpnService Integration**: Uses the official platform API to configure the network virtual interface (TUN `ParcelFileDescriptor`), DNS servers, MTU, and routing tables.
2. **Modern Jetpack Compose UI**: Dark neon cyber aesthetic, pulsating circular connect button, live connection timer, and bandwidth counters.
3. **Multi-Country Catalog**: Configured for 8 countries (United States, United Kingdom, Germany, Netherlands, Singapore, Canada, Japan, Australia).
4. **Transparent Development / Test Mode**: Ships with an explicit test mode that verifies UI, permission flow, foreground notification, and TUN interface creation without falsely claiming a third-party server connection.
5. **Real-World Backend Pluggable Architecture**: Clear separation of concern across `VpnManager`, `SecureShieldVpnService`, `ServerRepository`, and `SecurePreferencesManager` (using `EncryptedSharedPreferences`).
6. **Zero-PC Cloud CI/CD**: Includes a ready-to-use GitHub Actions workflow (`.github/workflows/build-apk.yml`) to automatically compile the APK in the cloud from an Android phone.

---

## 📂 Project Architecture

```
app/
├── src/main/
│   ├── java/com/secureshield/vpn/
│   │   ├── SecureShieldApp.kt               # Application entry, creates Notification Channel
│   │   ├── MainActivity.kt                  # Activity entry, edge-to-edge, permission dispatch
│   │   ├── model/
│   │   │   ├── VpnState.kt                  # Connection state machine & status enum
│   │   │   ├── VpnServer.kt                 # Server metadata & attributes
│   │   │   ├── VpnProtocol.kt               # WireGuard, OpenVPN, Test Mode definition
│   │   │   ├── ConnectionStats.kt           # Throughput, data counters, duration
│   │   │   └── UserSettings.kt              # App settings data structure
│   │   ├── data/
│   │   │   └── SecurePreferencesManager.kt  # AndroidX EncryptedSharedPreferences (AES-256)
│   │   ├── vpn/
│   │   │   ├── SecureShieldVpnService.kt    # Official Android VpnService implementation
│   │   │   ├── VpnActionReceiver.kt         # BroadcastReceiver for notification disconnect
│   │   │   └── VpnManager.kt                # High-level coordinator & StateFlow provider
│   │   ├── repository/
│   │   │   ├── ServerRepository.kt          # 8-country server provider
│   │   │   └── VpnRepository.kt             # Clean data layer facade
│   │   ├── ui/
│   │   │   ├── theme/                       # Color, Type, Theme (Material 3 Dark Palette)
│   │   │   ├── navigation/                  # NavRoutes & Compose NavHost
│   │   │   ├── viewmodel/                   # VpnViewModel & SettingsViewModel
│   │   │   └── screens/
│   │   │       ├── SplashScreen.kt          # Animated glowing shield splash
│   │   │       ├── HomeScreen.kt            # Circular connect button, timer, stats, server card
│   │   │       ├── ServerListScreen.kt      # Country search, flags, latency, selection
│   │   │       ├── SettingsScreen.kt        # Protocol switch, kill-switch link, auto-connect
│   │   │       ├── AboutScreen.kt           # Tech specs & version info
│   │   │       ├── PrivacyPolicyScreen.kt   # Google Play VPN disclosure compliance
│   │   │       └── TermsOfServiceScreen.kt  # Acceptable use agreement
│   │   └── utils/
│   │       └── Formatters.kt                # Byte & duration formatting utilities
│   ├── res/
│   │   ├── values/                          # strings.xml, colors.xml, themes.xml
│   │   ├── drawable/                        # ic_shield.xml, launcher foreground
│   │   └── mipmap-anydpi-v26/               # Adaptive launcher icons
│   └── AndroidManifest.xml                  # VpnService declaration, BIND_VPN_SERVICE permission
```

---

## 🚀 How to Build

### Option 1: On a Computer using Android Studio
1. Open Android Studio (Ladybug / Koala or newer).
2. Click **File -> Open** and select this directory (`SecureShieldVPN`).
3. Allow Gradle to synchronize dependencies.
4. Connect an Android phone with USB Debugging enabled (or start an emulator).
5. Click the green **Run (▶)** button.

### Option 2: On an Android Phone (No Computer Needed)
1. **GitHub Cloud Build (Easiest)**:
   - Upload or push this project to a free GitHub repository.
   - Go to the **Actions** tab on GitHub in your phone's browser.
   - The included `.github/workflows/build-apk.yml` workflow will automatically run and build `app-debug.apk`.
   - Download the APK from the workflow artifacts directly onto your phone and install it!
2. **On-Device IDE (AndroidIDE)**:
   - Install **AndroidIDE** from F-Droid or GitHub releases on your phone.
   - Import this folder and tap **Build APK**.
