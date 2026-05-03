# 🏃 Health Tracker - AI-Powered Personal Health Assistant
-------------------------------------------------------------
THIS PROJECT DEVELOPED BY TEAM "HUM JEET GAYE"
TABISH-> DEVELOPER
BHAVESH-> JR DEV
SHAHID-> BACKEND DEV
SUNNY-> JR BACKEND DEV
VIVEK-> UIUX & TESTING 

<p align="center">
  <img src="docs/assets/logo.png" alt="Health Tracker Logo" width="120"/>
</p>

<p align="center">
  <strong>Your Complete Health Companion with AI Avatar Assistant</strong>
</p>

<p align="center">
  <a href="#features">Features</a> •
  <a href="#screenshots">Screenshots</a> •
  <a href="#architecture">Architecture</a> •
  <a href="#installation">Installation</a> •
  <a href="#usage">Usage</a>
</p>

---

## 📱 Overview

Health Tracker is a comprehensive Android health monitoring application built with modern Android development practices. It features an innovative **Floating AI Avatar Assistant** that works even when the app is closed, real-time step counting, medical reminders, progress tracking, and social health circles.

### Key Highlights

- 🤖 **Floating AI Avatar** - Always-on assistant that appears over other apps
- 👟 **Background Step Counter** - Tracks steps even when app is closed
- 📊 **Real-time Progress Charts** - Beautiful visualizations of your health data
- 💊 **Medical Reminders** - Never miss your medications with smart alarms
- 👥 **Social Health Circles** - Connect and compete with friends
- 🎮 **Gamification** - Badges, streaks, and achievements to keep you motivated

---

## ✨ Features

### 🤖 Floating AI Avatar Assistant (F06)

The standout feature - a floating assistant that works **even when the app is closed**, similar to Facebook Messenger chat heads.

**Capabilities:**
- Voice commands: "How many steps?", "Set reminder", "Not feeling well"
- Text-to-Speech responses
- Quick action buttons: Voice, Open App, Steps, Remind, Unwell
- Draggable floating bubble
- Expandable panel with full controls

**Voice Commands Supported:**
| Command | Action |
|---------|--------|
| "How many steps" | Speaks your current step count |
| "Open app" / "Open health" | Opens the main app |
| "Set reminder" | Opens reminder screen |
| "Not feeling well" / "Sick" | Opens symptom triage |
| "Hide" / "Close" | Hides the avatar |
| "Hello" / "Hi" | Greeting response |

### 👟 Background Step Counter (F01-F02)

Continuous step tracking using device sensors, running as a foreground service.

**Features:**
- Real-time step counting using `TYPE_STEP_COUNTER` sensor
- Calorie calculation based on user profile
- Distance estimation
- Persistent notification showing current stats
- Auto-start on device boot
- Data saved to SharedPreferences for offline access

**Technical Details:**
```
Service: StepCounterService (Foreground Service)
Sensor: TYPE_STEP_COUNTER / TYPE_STEP_DETECTOR
Storage: SharedPreferences (step_counter_prefs, step_history_v3)
```

### 📊 Progress Dashboard (F03)

Beautiful charts and statistics showing your health journey.

**Includes:**
- Line charts for Steps, Calories, Distance
- Period selector: 7 / 14 / 30 days
- Goal achievement rings with animations
- Summary statistics (Average, Best Day, Active Days)
- Public/Private toggle for social sharing
- Friends progress cards (when public)

### 💊 Medical Reminders (F13)

Smart medication and health reminders with multiple fallback mechanisms.

**Features:**
- Exact alarm scheduling with `setAlarmClock()`
- WorkManager backup for MIUI/aggressive battery optimization
- Custom alarm sounds and vibration patterns
- Notification actions: Done, Snooze, Skip
- Test alarm functionality
- Boot receiver for rescheduling

### 👥 Social Health Circles (F11)

Connect with friends, family, or colleagues for group health tracking.

**Features:**
- Create/Join circles with invite codes
- Three circle types: Friends, Corporate, Family
- Leaderboards by steps, calories, distance
- Privacy controls per circle
- Challenges and competitions

### 🎮 Gamification (F10)

Keep users motivated with game-like elements.

**Includes:**
- Daily/Weekly/Monthly streaks
- Achievement badges
- Level progression
- Leaderboard rankings
- Streak risk notifications

### 🍎 Diet Tracking (F08)

AI-powered food recognition and nutrition logging.

**Features:**
- Camera-based food scanning
- Manual meal logging
- Calorie and macro tracking
- Meal history
- Diet plan recommendations

### 🧠 Mental Health (F09)

Wellness tracking for complete health monitoring.

**Features:**
- Mood logging
- Stress assessment
- Mindfulness reminders
- Wellness activity tracking

### 🏥 Health Triage (F12)

Symptom checker with clinic finder.

**Features:**
- Symptom input and analysis
- Specialist recommendations
- Nearby clinic finder with maps
- Urgency level assessment

---

## 🏗️ Architecture

### Clean Architecture with MVVM

```
┌─────────────────────────────────────────────────────────────┐
│                      Presentation Layer                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │   Screens   │  │  ViewModels │  │  Compose Components │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
├─────────────────────────────────────────────────────────────┤
│                       Domain Layer                           │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │  Use Cases  │  │   Models    │  │  Repository Interfaces│ │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
├─────────────────────────────────────────────────────────────┤
│                        Data Layer                            │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │    Room     │  │  Firebase   │  │   Health Connect    │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

### Module Structure

```
health-tracker/
├── app/                    # Main application module
│   ├── di/                 # Hilt dependency injection
│   ├── presentation/       # UI layer (Compose screens)
│   │   ├── avatar/         # AI Avatar components
│   │   ├── dashboard/      # Home dashboard
│   │   ├── diet/           # Diet tracking
│   │   ├── gamification/   # Achievements & badges
│   │   ├── medical/        # Medical records & reminders
│   │   ├── mentalhealth/   # Wellness tracking
│   │   ├── planning/       # Workout & diet plans
│   │   ├── progress/       # Progress charts
│   │   ├── social/         # Health circles
│   │   ├── triage/         # Symptom checker
│   │   └── theme/          # Material 3 theming
│   └── service/            # Background services
│       ├── avatar/         # Floating avatar service
│       ├── notification/   # Reminder services
│       └── step/           # Step counter service
│
├── domain/                 # Business logic module
│   ├── model/              # Domain models
│   ├── repository/         # Repository interfaces
│   └── usecase/            # Use case interfaces
│
├── data/                   # Data layer module
│   ├── local/              # Room database
│   │   ├── dao/            # Data access objects
│   │   └── entity/         # Database entities
│   ├── repository/         # Repository implementations
│   ├── security/           # Encryption & security
│   └── worker/             # WorkManager workers
│
└── ml/                     # Machine learning module
    └── FoodClassificationService
```

### Tech Stack

| Category | Technology |
|----------|------------|
| **Language** | Kotlin 1.9+ |
| **UI Framework** | Jetpack Compose + Material 3 |
| **Architecture** | MVVM + Clean Architecture |
| **DI** | Hilt |
| **Database** | Room |
| **Backend** | Firebase (Auth, Firestore, FCM) |
| **Health Data** | Health Connect API |
| **Background Work** | WorkManager + Foreground Services |
| **ML** | TensorFlow Lite |
| **Async** | Kotlin Coroutines + Flow |
| **Navigation** | Compose Navigation |

---

## 📲 Installation

### Prerequisites

- Android Studio Hedgehog (2023.1.1) or newer
- JDK 17
- Android SDK 34
- Kotlin 1.9+

### Build Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/health-tracker.git
   cd health-tracker
   ```

2. **Configure Firebase**
   - Create a Firebase project
   - Download `google-services.json`
   - Place it in `app/` directory

3. **Build the project**
   ```bash
   # Windows
   .\gradlew.bat assembleDebug
   
   # Linux/Mac
   ./gradlew assembleDebug
   ```

4. **Install on device**
   ```bash
   adb install -r app/build/outputs/apk/debug/app-debug.apk
   ```

### Quick Build Script (Windows)

```batch
@echo off
.\gradlew.bat assembleDebug
adb install -r "app\build\outputs\apk\debug\app-debug.apk"
adb shell am start -n com.healthtracker/.presentation.MainActivity
```

---

## 🚀 Usage

### First Launch

1. **Grant Permissions**
   - Activity Recognition (for step counting)
   - Notifications (for reminders)
   - Microphone (for voice commands)
   - Display over other apps (for floating avatar)

2. **Complete Onboarding**
   - Enter your profile (name, age, weight, height)
   - Select health goal (Weight Loss, Fitness, General)
   - Set daily step goal

3. **Enable Floating Avatar**
   - Tap the robot FAB button
   - Grant "Display over other apps" permission
   - Avatar will appear on screen

### MIUI/Xiaomi Specific Setup

For Xiaomi devices with aggressive battery optimization:

1. **Settings > Apps > Manage apps > Health Tracker**
   - Enable "Autostart"
   - Battery saver: "No restrictions"
   - Enable "Display pop-up windows while running in background"

2. **Lock the app in recent apps** (swipe down on the app card)

3. **Disable battery optimization**
   - Settings > Battery > App battery saver > Health Tracker > No restrictions

### Using the Floating Avatar

| Action | Result |
|--------|--------|
| Tap avatar bubble | Expand/collapse panel |
| Tap "Voice" button | Start voice recognition |
| Say "How many steps" | Hear your step count |
| Say "Open app" | Opens Health Tracker |
| Tap "Hide" | Removes avatar from screen |
| Notification "Hide" | Stops avatar service |

---

## 🔐 Permissions

| Permission | Purpose |
|------------|---------|
| `ACTIVITY_RECOGNITION` | Step counting |
| `POST_NOTIFICATIONS` | Reminders & alerts |
| `RECORD_AUDIO` | Voice commands |
| `SYSTEM_ALERT_WINDOW` | Floating avatar |
| `FOREGROUND_SERVICE` | Background step counting |
| `RECEIVE_BOOT_COMPLETED` | Auto-start services |
| `SCHEDULE_EXACT_ALARM` | Medical reminders |
| `CAMERA` | Food scanning |
| `ACCESS_FINE_LOCATION` | Clinic finder |
| `INTERNET` | Firebase sync |

---

## 📁 Key Files

### Services

| File | Description |
|------|-------------|
| `AvatarOverlayService.kt` | Floating AI avatar that works over other apps |
| `StepCounterService.kt` | Background step counting foreground service |
| `MedicalReminderNotificationService.kt` | Medication reminder scheduling |
| `BootReceiver.kt` | Restarts services after device boot |

### Screens

| File | Description |
|------|-------------|
| `DashboardScreen.kt` | Main home screen with stats |
| `ProgressScreen.kt` | Charts and progress tracking |
| `MedicalScreen.kt` | Medical records and reminders |
| `SocialScreen.kt` | Health circles and friends |
| `GamificationScreen.kt` | Achievements and badges |

### ViewModels

| File | Description |
|------|-------------|
| `DashboardViewModel.kt` | Dashboard state management |
| `ProgressViewModel.kt` | Progress data and charts |
| `MedicalViewModel.kt` | Medical records logic |

---

## 🎨 UI Theme

The app uses a premium dark theme with the following color palette:

```kotlin
// Primary Colors
val ElectricBlue = Color(0xFF3B82F6)
val CyberGreen = Color(0xFF10B981)
val NeonPurple = Color(0xFF8B5CF6)

// Background
val DarkBackground = Color(0xFF0D0D1A)
val CardBackground = Color(0xFF1A1A2E)

// Accent Colors
val WarningOrange = Color(0xFFF59E0B)
val ErrorRed = Color(0xFFEF4444)
val SuccessGreen = Color(0xFF10B981)
```

---

## 🧪 Testing

### Run Unit Tests
```bash
.\gradlew.bat test
```

### Run Instrumented Tests
```bash
.\gradlew.bat connectedAndroidTest
```

### Test Locations
- `app/src/test/` - Unit tests
- `app/src/androidTest/` - UI tests
- `domain/src/test/` - Domain layer tests
- `data/src/test/` - Data layer tests

---

## 📄 Documentation

| Document | Description |
|----------|-------------|
| [FEATURE_FLAGS.md](docs/FEATURE_FLAGS.md) | Feature flag configuration |
| [SECURITY_IMPLEMENTATION_SUMMARY.md](docs/SECURITY_IMPLEMENTATION_SUMMARY.md) | Security measures |
| [FIREBASE_TEST_LAB_SETUP.md](docs/FIREBASE_TEST_LAB_SETUP.md) | Firebase testing setup |

---

## 🔧 Configuration

### Feature Flags

Located in `FeatureFlagManager.kt`:

```kotlin
enum class FeatureFlag {
    AI_SUGGESTIONS,      // AI-powered health suggestions
    FOOD_SCANNING,       // Camera-based food recognition
    SOCIAL_CIRCLES,      // Health circles feature
    GAMIFICATION,        // Badges and achievements
    FLOATING_AVATAR,     // AI avatar overlay
    HEALTH_CONNECT       // Health Connect integration
}
```

### Build Variants

| Variant | Description |
|---------|-------------|
| `debug` | Development build with logging |
| `release` | Production build with ProGuard |

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Health Tracker Team**

---

## 🙏 Acknowledgments

- Material Design 3 for the beautiful UI components
- Jetpack Compose for modern Android UI
- Firebase for backend services
- Health Connect for standardized health data access

---

<p align="center">
  Made with ❤️ for a healthier world
</p>
