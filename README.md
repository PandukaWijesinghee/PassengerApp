# SmartTransit Passenger App 🚌

A comprehensive Flutter-based mobile application for bus transportation booking and real-time tracking. Passengers can search for trips, book seats, track buses in real-time, and manage their reservations with secure SMS OTP authentication.

##  Documentation

**New to this project?** Start here:

- **[Documentation Index](docs/INDEX.md)** - Complete guide to all documentation
- **[Getting Started](docs/GETTING_STARTED.md)** - Setup & quick overview (15 min)
- **[Architecture Guide](docs/ARCHITECTURE.md)** - How the app is structured (25 min)
- **[Screens Guide](docs/SCREENS.md)** - What each screen does (30 min)
- **[Development Guide](docs/DEVELOPMENT.md)** - Coding standards & patterns
- **[Bus Tracking Implementation](BUS_TRACKING_IMPLEMENTATION.md)** - Real-time tracking details

 **Most people should start with [Getting Started](docs/GETTING_STARTED.md)**

---

##  Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Project Structure](#project-structure)
- [Running the App](#running-the-app)
- [API Integration](#api-integration)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)
- [Documentation](#-documentation)
- [License](#license)

##  Features

###  Authentication
- **SMS OTP Login**: Secure authentication via one-time passwords (OTP)
- **Auto-Read SMS**: Automatic SMS reading on Android (with SMS Autofill)
- **JWT Tokens**: Access and refresh tokens for API security
- **Profile Management**: Complete profile setup and editing

###  Trip Management
- **Trip Search**: Search available buses by route, date, and time
- **Real-time Availability**: Live seat availability checking
- **Booking System**: Reserve seats with real-time confirmation
- **Booking History**: View all past and upcoming bookings
- **Cancellation**: Cancel bookings before departure (if allowed)

###  Real-Time Bus Tracking
- **Live Location Updates**: Track your booked bus in real-time (10-second polling)
- **Route Visualization**: View complete route on Google Maps with polylines
- **Trip Status**: See current bus status (not started, in transit, completed)
- **Speed Monitoring**: Display current bus speed in km/h
- **Location History**: View last location update timestamp

###  User Interface
- **Material Design**: Modern and responsive UI
- **Dark Mode Support**: Light and dark theme switching
- **Multiple Screens**: 
  - Splash screen with animated logo
  - Phone input with country code selection
  - OTP verification with auto-read
  - Profile completion
  - Home/Dashboard with carousel
  - Search results
  - Booking management
  - Bus tracking with maps
  - User profile

###  Additional Features
- **Google Maps Integration**: Real-time location tracking and route visualization
- **Supabase Integration**: Route polylines and real-time data synchronization
- **QR Code Support**: Digital ticketing display
- **WebView Support**: In-app browser for policies and external content
- **Device Info**: Tracking device information for analytics
- **Local Storage**: Secure token storage with Flutter Secure Storage
- **Image Carousel**: Featured buses and promotional banners

##  Prerequisites

Before you begin, ensure you have the following installed:

- **Flutter SDK**: Version 3.8.1 or higher
  - Download from [flutter.dev](https://flutter.dev/docs/get-started/install)
- **Dart SDK**: Included with Flutter (version 3.8.1+)
- **Android Studio** (for Android development)
  - Android SDK API level 21+
  - Gradle 8.12+
- **Xcode** (for iOS development - macOS only)
- **Git**: For version control

### Key Dependencies

This app uses the following major Flutter packages:

**State Management & Architecture:**
- `provider: ^6.1.1` - State management

**Networking & API:**
- `http: ^1.1.0` - HTTP client
- `dio: ^5.4.0` - Advanced HTTP client

**Storage:**
- `flutter_secure_storage: ^9.0.0` - Secure token storage
- `shared_preferences: ^2.2.2` - Local key-value storage

**Maps & Location:**
- `google_maps_flutter: ^2.13.1` - Google Maps integration
- `geolocator: ^14.0.2` - Device location services
- `supabase_flutter: ^2.10.3` - Supabase client for route data

**Authentication:**
- `sms_autofill: ^2.4.0` - SMS OTP auto-reading
- `intl_phone_field: ^3.2.0` - International phone number input
- `pinput: ^3.0.1` - OTP input widget

**UI Components:**
- `flutter_spinkit: ^5.2.0` - Loading animations
- `carousel_slider: ^5.1.1` - Image carousels
- `qr_flutter: ^4.1.0` - QR code generation
- `webview_flutter: ^4.13.0` - In-app browser

**Utilities:**
- `intl: ^0.18.1` - Internationalization
- `logger: ^2.0.2` - Logging
- `device_info_plus: ^10.1.0` - Device information
- `package_info_plus: ^8.0.0` - App package info
- `uuid: ^4.5.1` - UUID generation
- `flutter_dotenv: ^5.1.0` - Environment variables

### Verify Installation
```bash
flutter --version
dart --version
flutter doctor
```

##  Installation

### 1. Clone or Navigate to the Repository
```bash
cd c:\Users\pandu\Documents\AASL\Workspace\For_Share\PassengerApp
```

### 2. Get Flutter Dependencies
```bash
flutter pub get
```

### 3. Generate Build Files
```bash
flutter pub run build_runner build
```

### 4. Install Platform-Specific Dependencies

**For Android:**
```bash
# No additional steps needed - Gradle handles it
```

**For iOS (macOS only):**
```bash
cd ios
pod install
cd ..
```

##  Configuration

### 1. Environment Variables

Create a `.env` file in the project root:

```bash
cp .env.example .env
```

Edit `.env` and configure:

```dotenv
# Supabase Configuration (for route polylines and real-time data)
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your_supabase_anon_key_here

# Google Maps API Key (required for location features and bus tracking)
GOOGLE_MAPS_API_KEY=your_google_maps_api_key_here

# Backend API Configuration
# Choreo production URL or your backend server URL
API_BASE_URL=https://your-backend-api-url/v1.0
```

**Important Notes:**
- Get Supabase credentials from [supabase.com](https://supabase.com)
- Get Google Maps API key from [Google Cloud Console](https://console.cloud.google.com/apis/credentials)
- Ensure your backend API is running and accessible
- Never commit the `.env` file to version control

### 2. Android Configuration

**Update `android/app/src/main/AndroidManifest.xml`:**
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.READ_SMS" />
<uses-permission android:name="android.permission.RECEIVE_SMS" />
```

**Add Google Maps (required for bus tracking):**
```xml
<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="YOUR_GOOGLE_MAPS_API_KEY" />
```

### 3. iOS Configuration

**Update `ios/Runner/Info.plist`:**
```xml
<key>NSLocationWhenInUseUsageDescription</key>
<string>This app needs your location to show nearby transit routes and track buses</string>
<key>NSLocationAlwaysUsageDescription</key>
<string>This app needs location access to provide real-time bus tracking</string>
<key>NSCameraUsageDescription</key>
<string>Camera is used to scan QR codes for tickets</string>
```

##  Project Structure

```
lib/
├── main.dart                 # App entry point
├── config/
│   ├── api_config.dart      # API endpoints and configuration
│   ├── constants.dart       # App-wide constants
│   └── theme_config.dart    # Theme configuration
├── models/
│   ├── auth_models.dart     # Authentication models
│   ├── booking_models.dart  # Booking data models
│   ├── trip_models.dart     # Trip and schedule models
│   └── user_models.dart     # User profile models
├── providers/
│   ├── auth_provider.dart       # Authentication state management
│   ├── booking_intent_provider.dart  # Booking flow management
│   ├── search_provider.dart     # Trip search state
│   ├── theme_provider.dart      # Theme switching
│   └── user_provider.dart       # User profile state
├── screens/
│   ├── splash_screen.dart       # Splash/loading screen
│   ├── auth/
│   │   ├── phone_input_screen.dart      # Phone entry
│   │   ├── otp_verification_screen.dart # OTP verification
│   │   └── complete_profile_screen.dart # Profile setup
│   ├── home/
│   │   ├── home_screen.dart         # Main dashboard
│   │   ├── search_screen.dart       # Search trips
│   │   └── booking_screen.dart      # Booking details
│   └── profile/
│       ├── profile_screen.dart      # User profile
│       ├── edit_profile_screen.dart # Edit profile
│       └── help_and_support.dart    # Support page
├── services/
│   ├── api_service.dart         # HTTP client and API calls
│   ├── auth_service.dart        # Authentication logic
│   ├── booking_service.dart     # Booking operations
│   └── search_service.dart      # Trip search operations
├── theme/
│   ├── app_colors.dart          # Color palette
│   └── app_typography.dart      # Typography styles
├── utils/
│   ├── validators.dart          # Input validation
│   ├── storage_helper.dart      # Secure storage
│   └── logger.dart              # Logging utilities
└── widgets/
    ├── custom_app_bar.dart      # Reusable app bar
    ├── custom_button.dart       # Button components
    └── loading_widget.dart      # Loading indicators
```

##  Running the App

### 1. Run on Android Emulator/Device
```bash
# List connected devices
flutter devices

# Run on default device
flutter run

# Run on specific device
flutter run -d <device_id>

# Run in release mode
flutter run --release
```

### 2. Run on iOS (macOS only)
```bash
flutter run -d iphone
```

### 3. Run on Web
```bash
flutter run -d chrome
```

### 4. Run with Hot Reload
```bash
# Press 'r' in the terminal for hot reload
# Press 'R' for hot restart
# Press 'q' to quit
```

## 🔌 API Integration

### Authentication Flow

1. **Send OTP**
   ```
   POST /api/v1/auth/send-otp
   {
     "phone_number": "+94785957049"
   }
   Response: { "otp": "123456", "expires_at": "..." }
   ```

2. **Verify OTP**
   ```
   POST /api/v1/auth/verify-otp
   {
     "phone_number": "+94785957049",
     "otp": "123456"
   }
   Response: { "access_token": "...", "refresh_token": "..." }
   ```

3. **Use Access Token**
   ```
   Headers:
   Authorization: Bearer <access_token>
   ```

### Key Endpoints

| Method | Endpoint | Purpose |
|--------|----------|---------|
| GET | `/health` | Health check |
| POST | `/api/v1/auth/send-otp` | Send OTP |
| POST | `/api/v1/auth/verify-otp` | Verify OTP & get tokens |
| GET | `/api/v1/user/profile` | Get user profile |
| PUT | `/api/v1/user/profile` | Update user profile |
| POST | `/api/v1/search` | Search trips |
| POST | `/api/v1/bookings` | Create booking |
| GET | `/api/v1/bookings` | List user bookings |
| GET | `/api/v1/bookings/{id}` | Get booking details |
| DELETE | `/api/v1/bookings/{id}` | Cancel booking |
| GET | `/api/v1/active-trips/by-scheduled-trip/:id` | Get real-time bus location |

### Bus Tracking API

**Get Active Trip by Scheduled Trip ID:**
```
GET /api/v1/active-trips/by-scheduled-trip/:scheduled_trip_id
Headers: Authorization: Bearer <token>

Response:
{
  "has_active_trip": true,
  "active_trip": {
    "id": "...",
    "scheduled_trip_id": "...",
    "current_latitude": 6.9271,
    "current_longitude": 79.8612,
    "last_location_update": "2024-01-01T10:30:00Z",
    "current_speed_kmh": 45.5,
    "status": "in_transit"
  }
}
```

### See Backend Documentation
For complete API documentation, visit the backend's swagger.yaml file or access the Postman collection.

##  Testing

### Unit Tests
```bash
# Run all unit tests
flutter test

# Run specific test file
flutter test test/unit_tests.dart

# Run with coverage
flutter test --coverage
```

### Widget Tests
```bash
# Run all widget tests
flutter test

# Run specific widget test
flutter test test/widget_test.dart
```

### Integration Tests
```bash
flutter test integration_test/
```

### Manual Testing Checklist
- [ ] Login with valid phone number
- [ ] OTP auto-read works on Android
- [ ] OTP manual entry works
- [ ] Profile completion saves data
- [ ] Search returns results
- [ ] Booking flow completes successfully
- [ ] Real-time bus tracking displays on map
- [ ] Bus location updates every 10 seconds
- [ ] Route polyline displays correctly
- [ ] Dark mode toggle works
- [ ] App handles network errors gracefully
- [ ] Session refresh with refresh token works
- [ ] Logout clears all data
- [ ] QR code displays for bookings
- [ ] Carousel images load correctly

##  Troubleshooting

### Common Issues

**1. Build Fails with Gradle Error**
```bash
# Clean and rebuild
flutter clean
flutter pub get
flutter pub run build_runner clean
flutter pub run build_runner build
```

**2. Android Build Error: "minSdkVersion"**
- Edit `android/app/build.gradle.kts`
- Ensure `minSdkVersion = 21` or higher

**3. iOS Pod Installation Fails**
```bash
cd ios
rm -rf Pods
rm Podfile.lock
pod install
cd ..
```

**4. API Connection Fails**
- Verify backend is running
- Check `.env` file has correct `API_BASE_URL`
- Check device can reach the API (firewall/network)
- View logs with: `flutter logs`

**5. SMS OTP Not Auto-Reading on Android**
- Run: `flutter run -t lib/get_app_hash.dart`
- Copy the app hash from console
- Update `PASSENGER_APP_HASH` in backend `.env`
- Redeploy backend

**6. Google Maps Not Showing**
- Verify `GOOGLE_MAPS_API_KEY` in `.env` file
- Check API key has Maps SDK for Android/iOS enabled
- Ensure billing is enabled in Google Cloud Console
- Check AndroidManifest.xml has the API key configured

**7. Supabase Connection Issues**
- Verify `SUPABASE_URL` and `SUPABASE_ANON_KEY` in `.env`
- Check Supabase project is active
- Ensure route polylines table exists in Supabase
- Test connection with: `flutter run -v`

**8. Bus Tracking Not Working**
- Check if active trip exists for scheduled trip
- Verify backend active trips API is running
- Ensure location permissions are granted
- Check network connectivity

**9. Secure Storage Errors**
- For Android: Ensure Android Keystore is available
- For iOS: Check Keychain access permissions
- Clear app data and reinstall if persistent

**10. Environment Variables Not Loading**
- Ensure `.env` file exists in project root
- Check file name is exactly `.env` (not `.env.txt`)
- Rebuild app after changing `.env`: `flutter clean && flutter run`

### Debug Mode

Enable detailed logging:
```bash
# View all app logs
flutter logs

# Run with verbose output
flutter run -v

# Debug on Android emulator
adb logcat | grep flutter
```

##  Additional Resources

- [Flutter Documentation](https://flutter.dev/docs)
- [Dart Language Tour](https://dart.dev/guides/language/language-tour)
- [Provider Package](https://pub.dev/packages/provider)
- [Google Maps Flutter Plugin](https://pub.dev/packages/google_maps_flutter)
- [Supabase Flutter Documentation](https://supabase.com/docs/reference/dart/introduction)
- [Firebase Security Best Practices](https://firebase.google.com/docs/best-practices)

##  App Information

**Version:** 2.0.0+1  
**Package Name:** sms_auth_passenger_app  
**Supported Platforms:** Android, iOS, Web (partial), Windows, macOS, Linux  
**Minimum Android SDK:** 21 (Android 5.0 Lollipop)  
**Target Android SDK:** Latest

##  Architecture Highlights

- **Clean Architecture**: Separation of concerns with providers, services, and models
- **State Management**: Provider pattern for reactive state updates
- **API Layer**: Centralized API service with interceptors and error handling
- **Secure Storage**: Encrypted storage for sensitive data (tokens, user info)
- **Real-time Updates**: Polling mechanism for live bus tracking (10-second intervals)
- **Offline Support**: Local caching of booking data and user profiles

##  Security Features

- JWT-based authentication with refresh token rotation
- Secure storage for sensitive credentials
- HTTPS-only API communication
- Phone number verification via SMS OTP
- Auto-logout on token expiration
- Device fingerprinting for security

##  Key Workflows

1. **User Registration/Login:**
   - Enter phone number → Receive OTP → Verify OTP → Complete profile

2. **Trip Booking:**
   - Search trips → View results → Select trip → Choose seats → Confirm booking

3. **Bus Tracking:**
   - View bookings → Select active booking → Track bus in real-time on map

4. **Profile Management:**
   - View profile → Edit information → Update preferences → Save changes

##  Contributing

1. Create a feature branch: `git checkout -b feature/your-feature`
2. Follow Flutter style guide and linting rules
3. Write tests for new features
4. Commit changes: `git commit -am 'Add feature'`
5. Push to branch: `git push origin feature/your-feature`
6. Create Pull Request with detailed description

##  Known Issues

- WebView may have rendering issues on some Android devices
- SMS auto-read requires app hash configuration on backend
- iOS location permissions require "Always" access for background tracking

##  Future Enhancements

- [ ] Push notifications for trip updates
- [ ] Multi-language support (Sinhala, Tamil)
- [ ] Offline mode with local database
- [ ] Payment gateway integration
- [ ] Loyalty points and rewards system
- [ ] Route suggestions based on user history
- [ ] Social sharing of trips
- [ ] In-app chat support

##  License

This project is proprietary and confidential. All rights reserved.

---

**Questions or Issues?**
- Check the [Troubleshooting](#-troubleshooting) section above
- Review [Bus Tracking Implementation](BUS_TRACKING_IMPLEMENTATION.md) for tracking features
- Consult the [Documentation Index](docs/INDEX.md) for detailed guides
- Contact the development team

**Made with ❤️ using Flutter**
