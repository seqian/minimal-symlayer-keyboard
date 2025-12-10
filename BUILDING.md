# Building Minimal SymLayer Keyboard

This document explains how to build the Minimal SymLayer Keyboard APK from source so you can test and customize it on your Android device.

## Prerequisites

You'll need the following installed on your system:

1. **Java Development Kit (JDK) 17 or higher**
   - Download from [Oracle](https://www.oracle.com/java/technologies/downloads/) or use [OpenJDK](https://openjdk.org/)
   - Verify installation: `java -version`

2. **Android SDK** (optional, but recommended)
   - Install [Android Studio](https://developer.android.com/studio) which includes the Android SDK
   - Or install the [Android SDK Command-line Tools](https://developer.android.com/studio#command-tools) standalone

3. **Git** (to clone the repository)
   - Download from [git-scm.com](https://git-scm.com/downloads)

## Building from Command Line

### Step 1: Clone the Repository

```bash
git clone https://github.com/seqian/minimal-symlayer-keyboard.git
cd minimal-symlayer-keyboard
```

### Step 2: Build the APK

The project includes a Gradle wrapper (`gradlew` on Linux/Mac, `gradlew.bat` on Windows) that handles the build process automatically.

#### On Linux/Mac:

```bash
./gradlew assembleDebug
```

#### On Windows:

```cmd
gradlew.bat assembleDebug
```

**Note:** The first build may take several minutes as Gradle downloads dependencies.

### Step 3: Locate the Built APK

After a successful build, you'll find the APK files in:

- **Debug APK**: `app/build/outputs/apk/debug/app-debug.apk`

This APK includes a `.dev` suffix in the application ID to allow installation alongside release versions.

### Building a Release APK

For a release version (unsigned, using debug signing):

```bash
./gradlew assembleRelease
```

The release APK will be at: `app/build/outputs/apk/release/app-release.apk`

**Note:** The current configuration uses debug signing for release builds. For production releases, you should configure proper signing in `app/build.gradle.kts`.

## Building with Android Studio

### Step 1: Open the Project

1. Launch Android Studio
2. Select **File > Open**
3. Navigate to the cloned repository folder and click **OK**
4. Wait for Android Studio to sync the project with Gradle files

### Step 2: Build the APK

1. Select **Build > Build Bundle(s) / APK(s) > Build APK(s)** from the menu
2. Wait for the build to complete
3. Android Studio will show a notification with a link to locate the APK

Alternatively, you can use the **Run** button to build and install directly to a connected device.

## Installing the APK on Your Device

### Method 1: Via ADB (Android Debug Bridge)

If you have ADB installed:

```bash
adb install app/build/outputs/apk/debug/app-debug.apk
```

### Method 2: Direct Transfer

1. Copy the APK file to your Android device (via USB, cloud storage, or email)
2. On your device, open the file manager and tap the APK file
3. Follow the on-screen prompts to install
4. You may need to enable "Install from Unknown Sources" in your device settings

### Method 3: From Android Studio

1. Connect your Android device via USB with USB debugging enabled
2. Select **Run > Run 'app'** or click the green play button
3. Select your device from the list
4. Android Studio will build, install, and launch the app

## Enabling the Keyboard

After installation:

1. Go to **Settings > System > Languages & input > Virtual keyboard > Manage keyboards**
2. Enable **Minimal Symlayer Input**
3. Return to **Languages & input** and select **Minimal Symlayer Input** as your default input method

## Cleaning the Build

To clean build artifacts and start fresh:

```bash
./gradlew clean
```

## Troubleshooting

### Build Fails with "SDK location not found"

Create a `local.properties` file in the project root with:

```properties
sdk.dir=/path/to/your/android/sdk
```

Replace `/path/to/your/android/sdk` with your actual Android SDK location:
- **Linux/Mac**: Usually `~/Android/Sdk` or `~/Library/Android/sdk`
- **Windows**: Usually `C:\Users\YourUsername\AppData\Local\Android\Sdk`

### Build Fails with Java Version Error

Ensure you're using JDK 17 or higher. Check with:

```bash
java -version
```

If needed, set `JAVA_HOME` environment variable to point to your JDK installation.

### Gradle Daemon Issues

If you encounter Gradle daemon issues, try:

```bash
./gradlew --stop
./gradlew assembleDebug
```

## Customizing the Build

### Changing Version Name/Code

Edit `app/build.gradle.kts`:

```kotlin
versionCode = 1
versionName = "0.84"
```

### Modifying Application ID

The debug build uses the suffix `.dev` to allow side-by-side installation with release versions. To change this, edit `app/build.gradle.kts`:

```kotlin
debug {
    applicationIdSuffix = ".dev"  // Change or remove this
}
```

## Additional Resources

- [Android Developer Documentation](https://developer.android.com/studio/build)
- [Gradle Build Tool](https://gradle.org/)
- [Original TitanPocketKeyboard Project](https://github.com/oin/titanpocketkeyboard)

## Contributing

If you make improvements to the build process or this documentation, please consider contributing them back to the project!
