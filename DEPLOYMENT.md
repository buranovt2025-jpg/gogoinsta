# GoGoInsta - Deployment Guide

## 📱 Download APK

### Option 1: GitHub Actions (Recommended)

1. Go to the [Actions tab](https://github.com/buranovt2025-jpg/gogoinsta/actions) in this repository
2. Click on "Build Android APK" workflow
3. Select the latest successful run
4. Scroll down to **Artifacts** section
5. Click on `gogoinsta-release-apk` to download

### Option 2: Download Page

Visit our download page: **https://buranovt2025-jpg.github.io/gogoinsta/**

## 🔧 Installation Steps

### Android (APK)

1. **Download** the APK file to your Android device
2. **Open** the downloaded file
3. **Enable Unknown Sources** if prompted:
   - Go to **Settings** → **Security**
   - Enable **"Install unknown apps"** for your browser/file manager
4. **Tap Install** and wait for completion
5. **Open** GoGoInsta and enjoy!

## 🏗️ Building Locally

### Prerequisites
- Flutter SDK 3.24.0 or later
- Android Studio with SDK
- Java 17

### Build Commands

```bash
# Get dependencies
flutter pub get

# Create .env files (required)
cp packages/env/.env.example packages/env/.env
cp packages/env/.env packages/env/.env.dev
cp packages/env/.env packages/env/.env.prod

# Run build_runner for generated code
cd packages/env && dart run build_runner build --delete-conflicting-outputs
cd ../..

# Build debug APK
flutter build apk --debug -t lib/main_development.dart

# Build release APK
flutter build apk --release -t lib/main_development.dart
```

### Output Location
- Debug APK: `build/app/outputs/flutter-apk/app-debug.apk`
- Release APK: `build/app/outputs/flutter-apk/app-release.apk`

## 🔐 GitHub Secrets Required

For CI/CD to work, add these secrets in your GitHub repository settings:

| Secret | Description |
|--------|-------------|
| `SUPABASE_URL` | Your Supabase project URL |
| `SUPABASE_ANON_KEY` | Supabase anonymous key |
| `POWERSYNC_URL` | PowerSync URL (optional) |
| `FCM_SERVER_KEY` | Firebase Cloud Messaging key |
| `WEB_CLIENT_ID` | Google OAuth Web Client ID |
| `IOS_CLIENT_ID` | Google OAuth iOS Client ID |

## 📄 GitHub Pages Setup

To enable the download page:

1. Go to **Settings** → **Pages** in your GitHub repository
2. Under **Source**, select **GitHub Actions**
3. The page will be deployed automatically on push to main
4. Access at: `https://buranovt2025-jpg.github.io/gogoinsta/`

## 🔄 Automatic Builds

APKs are automatically built on:
- Every push to `main` branch
- Every pull request to `main`
- Manual trigger via GitHub Actions

## 📋 Troubleshooting

### Build Fails with "Missing .env"
Ensure GitHub secrets are configured correctly.

### APK Won't Install
- Enable "Install unknown apps" in Android settings
- Check if your Android version is compatible (API 21+)

### App Crashes on Startup
- Check if `.env` variables are correctly set
- Verify `google-services.json` is present

## 📞 Support

For issues, please [create a GitHub issue](https://github.com/buranovt2025-jpg/gogoinsta/issues).
