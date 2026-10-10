# MAD Practical 4: Alarm Manager & Foreground Service Application
**Android | Kotlin | Gradle | API**

## 🎯 Aim
Create an Android Alarm application by using Service & Broadcast Receiver.

---

## 📱 Project Overview
**MAD Practical 4** is an Android application designed to demonstrate the complete lifecycle of scheduling, triggering, and controlling background system alarms.

The application integrates core Android framework components:
- **`AlarmManager`** for scheduling precise time-based wakeups.
- **`BroadcastReceiver`** (`AlarmBroadcastReceiver.kt`) to capture scheduled alarm intents even when the application is not actively running.
- **`Service`** (`AlarmService.kt`) with looping audio playback via `MediaPlayer` (`res/raw/alarm.mp3`).
- **Material 3 UI** featuring interactive cards, live digital clock (`TextClock`), time picker dialog, and dynamic card visibility.

---

## 📸 Component Architecture & Roles

### **`MainActivity.kt`**
- **Clock & Time Picker:** Binds `TimePickerDialog` to allow the user to select alarm time.
- **Smart Date Rollover:** Automatically detects if the chosen time has already passed for the current day; if so, increments the calendar by 1 day (`calendar.add(Calendar.DATE, 1)`).
- **AlarmManager Integration:** Creates an immutable `PendingIntent` targeted to `AlarmBroadcastReceiver` and triggers `alarmManager.setExact(AlarmManager.RTC_WAKEUP, ...)` with fallback checks for `SCHEDULE_EXACT_ALARM`.

### **`AlarmBroadcastReceiver.kt`**
- Extends `BroadcastReceiver` and acts as the bridge between `AlarmManager` and `AlarmService`.
- Reads the intent extra (`"Service1"`).
- On `"Start"`, invokes `context.startService(...)` to start `AlarmService`.
- On `"Stop"`, forwards the stop command using `context.stopService(...)`.

### **`AlarmService.kt`**
- Extends `Service`.
- Plays the alarm audio file located in `res/raw/alarm.mp3` using `MediaPlayer` with `isLooping = true`.
- Cleans up resources, stops audio playback, and releases memory in `onDestroy()`.

### **`activity_main.xml`**
- Encapsulated inside `ScrollView` and `ConstraintLayout` for responsive UI sizing.
- Built with Material 3 components: `MaterialCardView`, `MaterialButton`, `ImageView` vector banners, and native `TextClock`.

---

## 🔒 Android Permissions & Compliance

| Permission | Reason for Use |
| :--- | :--- |
| `android.permission.SCHEDULE_EXACT_ALARM` | Enables exact timestamp triggers using `AlarmManager.setExact()`. |

---

## 🚀 Getting Started & Installation

### 1. Clone the Repository
```bash
git clone https://github.com/Hetpatel318/24012011207_MAD_Practical4.git
```

### 2. Open in Android Studio
1. Launch Android Studio.
2. Select **Open** and navigate to the project directory `24012011207_MAD_Practical4`.
3. Allow Android Studio to complete Gradle sync and download required dependencies.

### 3. Build and Run
- Connect an Android device (via USB/Wi-Fi debugging) or start an AVD emulator (API 24+).
- Click **Run** (`Shift + F10`) in Android Studio.

---

## 🛠️ Tech Stack & Dependencies

- **Language:** Kotlin
- **UI Framework:** Android XML Layouts with Material Components (Material 3)
- **Minimum SDK:** API 24 (Android 7.0 Nougat)
- **Target SDK:** API 36
- **Key Libraries:**
  - `androidx.core:core-ktx:1.15.0`
  - `androidx.appcompat:appcompat:1.8.0`
  - `com.google.android.material:material:1.14.0`
  - `androidx.activity:activity-ktx:1.13.0`
  - `androidx.constraintlayout:constraintlayout:2.2.2`

---

## 👤 Author & Submission Information

- **Submitted by:** Het Patel
- **Enrollment Number:** 24012011207
- **Repository Link:** [https://github.com/Hetpatel318/24012011207_MAD_Practical4.git](https://github.com/Hetpatel318/24012011207_MAD_Practical4.git)
