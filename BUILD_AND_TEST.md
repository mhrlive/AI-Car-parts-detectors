# Building and Testing the AI Car Parts Detector

## Prerequisites

Before building the app, ensure you have:

1. **Android Studio** (Arctic Fox or later recommended)
2. **JDK 8 or higher**
3. **Android SDK** with the following:
   - Android SDK Platform 34
   - Android SDK Build-Tools 34.0.0+
   - Android SDK Platform-Tools

## Build Instructions

### Using Android Studio

1. **Open the Project**
   - Launch Android Studio
   - Click "Open an Existing Project"
   - Navigate to the project directory and select it

2. **Sync Gradle Files**
   - Android Studio should automatically prompt to sync Gradle
   - If not, click "File" → "Sync Project with Gradle Files"
   - Wait for the sync to complete

3. **Build the Project**
   - Click "Build" → "Make Project" or press `Ctrl+F9` (Windows/Linux) or `Cmd+F9` (Mac)
   - Wait for the build to complete

4. **Run on Device/Emulator**
   - Connect an Android device with USB debugging enabled, or start an Android Emulator
   - Click the "Run" button (green triangle) or press `Shift+F10`
   - Select your target device from the list
   - The app will install and launch automatically

### Using Command Line

1. **Navigate to Project Directory**
   ```bash
   cd AI-Car-parts-detectors
   ```

2. **Build Debug APK**
   ```bash
   ./gradlew assembleDebug
   ```
   The APK will be generated at: `app/build/outputs/apk/debug/app-debug.apk`

3. **Build Release APK** (requires signing configuration)
   ```bash
   ./gradlew assembleRelease
   ```

4. **Install on Connected Device**
   ```bash
   ./gradlew installDebug
   ```

## Testing the App

### Manual Testing Steps

1. **Launch the App**
   - The app will request camera permissions
   - Grant the camera permission when prompted

2. **Test Camera Capture**
   - Point the camera at a car engine or parts
   - Tap "TAKE PHOTO" button
   - The captured image should appear on screen
   - Detection results will appear at the bottom after processing

3. **Test Gallery Selection**
   - Tap "SELECT IMAGE" button
   - Choose an image from your device gallery
   - The selected image should appear on screen
   - Detection results will appear at the bottom after processing

4. **Verify Results**
   - Check that detected parts are listed with confidence scores
   - Results should be formatted as "Part Name: XX.X%"
   - The results section should be visible at the bottom

### Testing Checklist

- [ ] App launches successfully
- [ ] Camera permission is requested on first launch
- [ ] Camera preview is visible and responsive
- [ ] "TAKE PHOTO" button captures images correctly
- [ ] "SELECT IMAGE" button opens gallery
- [ ] Selected/captured images are displayed correctly
- [ ] Detection processing shows loading indicator
- [ ] Results are displayed with part names and confidence scores
- [ ] App handles orientation changes gracefully
- [ ] App handles permission denial appropriately

## Running Unit Tests

Currently, the project includes basic test infrastructure. To run tests:

```bash
./gradlew test
```

## Running Instrumented Tests

To run instrumented tests on a connected device or emulator:

```bash
./gradlew connectedAndroidTest
```

## Common Build Issues

### Issue: Gradle Sync Failed
**Solution:** Ensure you have an active internet connection and all required SDK components are installed.

### Issue: SDK Not Found
**Solution:** Set the `ANDROID_HOME` environment variable to your Android SDK location:
- Windows: `C:\Users\YourName\AppData\Local\Android\Sdk`
- Mac/Linux: `~/Library/Android/sdk` or `~/Android/Sdk`

### Issue: Build Tools Version Not Found
**Solution:** Open Android Studio → SDK Manager → SDK Tools and install the required Build Tools version.

### Issue: Kotlin Plugin Not Found
**Solution:** The project uses Kotlin 1.9.0. Ensure your Android Studio supports this version or update accordingly.

## Adding a Custom TensorFlow Lite Model

To use your own trained model:

1. Place your `.tflite` model file in: `app/src/main/assets/car_parts_model.tflite`
2. Update the labels file at: `app/src/main/assets/labels.txt`
3. Each line in labels.txt should correspond to a class in your model
4. Rebuild and run the app

If no model is present, the app will use mock detections for demonstration.

## Performance Tips

- For better detection accuracy, ensure good lighting when taking photos
- Hold the camera steady to avoid blurry images
- Get close enough to capture clear details of parts
- The app processes images in a background thread to maintain UI responsiveness

## Troubleshooting

### Camera Not Working
- Check that camera permissions are granted in device settings
- Ensure the device has a functioning camera
- Try restarting the app

### Detection Not Working
- Verify the TensorFlow Lite model is in the assets folder
- Check logcat for error messages: `adb logcat | grep CarPartsDetector`
- Ensure the labels.txt file matches your model's output classes

### App Crashes
- Check logcat for crash reports: `adb logcat | grep AndroidRuntime`
- Ensure device meets minimum SDK requirements (API 24+)
- Verify all required permissions are granted
