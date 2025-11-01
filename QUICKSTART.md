# Quick Start Guide

Get started with AI Car Parts Detector in 5 minutes!

## For End Users

### Installation

1. **Download** the APK from releases
2. **Enable** installation from unknown sources (if needed)
3. **Install** the app
4. **Launch** AI Car Parts Detector

### First Time Setup

1. **Grant Permissions**
   - Camera permission: Required
   - Storage permission: Optional (for gallery access)

2. **Start Using**
   - The app is ready to use immediately!
   - No account or internet connection required

### Using the App

#### Method 1: Take a Photo
1. Point camera at car engine parts
2. Tap **TAKE PHOTO** button
3. Wait for detection (< 1 second)
4. View results at the bottom

#### Method 2: Select from Gallery
1. Tap **SELECT IMAGE** button
2. Choose an image from your gallery
3. Wait for detection (< 1 second)
4. View results at the bottom

### Reading Results

Results appear as:
```
Battery: 92.3%
Alternator: 87.5%
Engine Block: 84.2%
```

- **Part Name**: Identified component
- **Percentage**: Detection confidence (higher is better)
- Results show top 5 detections above 30% confidence

### Tips for Best Results

✅ **Do:**
- Use good lighting
- Get close to parts
- Hold camera steady
- Capture clear, focused images
- Show multiple parts in frame

❌ **Don't:**
- Take photos in very dark conditions
- Use extremely blurry images
- Take photos from too far away

## For Developers

### Quick Setup

```bash
# Clone repository
git clone https://github.com/mhrlive/AI-Car-parts-detectors.git
cd AI-Car-parts-detectors

# Open in Android Studio
# File → Open → Select project folder

# Build and run
# Click Run button or press Shift+F10
```

### Adding Your Model

1. Place model file:
   ```
   app/src/main/assets/car_parts_model.tflite
   ```

2. Update labels:
   ```
   app/src/main/assets/labels.txt
   ```

3. Rebuild and run!

### Project Structure

```
AI-Car-parts-detectors/
├── app/
│   ├── src/main/
│   │   ├── java/com/carparts/detector/
│   │   │   ├── MainActivity.kt          # Main UI
│   │   │   └── CarPartsDetector.kt      # AI logic
│   │   ├── res/
│   │   │   └── layout/activity_main.xml # UI layout
│   │   └── assets/
│   │       └── labels.txt               # Part names
│   └── build.gradle                     # Dependencies
└── README.md                            # Documentation
```

### Key Files

- **MainActivity.kt**: Camera & UI logic
- **CarPartsDetector.kt**: TensorFlow Lite inference
- **activity_main.xml**: UI layout
- **labels.txt**: Car parts list
- **build.gradle**: Dependencies config

### Common Tasks

#### Change Detection Threshold
```kotlin
// In CarPartsDetector.kt
private const val CONFIDENCE_THRESHOLD = 0.3f // Change this
```

#### Change Max Results
```kotlin
// In CarPartsDetector.kt
private const val MAX_RESULTS = 5 // Change this
```

#### Change Input Size
```kotlin
// In CarPartsDetector.kt
private const val INPUT_SIZE = 224 // Change this
```

#### Add New Part Labels
```
// In app/src/main/assets/labels.txt
Engine Block
Battery
Your New Part Here  # Add here
```

### Building APK

```bash
# Debug APK
./gradlew assembleDebug

# Release APK (requires signing)
./gradlew assembleRelease

# Output location
app/build/outputs/apk/
```

### Running Tests

```bash
# Unit tests
./gradlew test

# Instrumented tests
./gradlew connectedAndroidTest
```

## Troubleshooting

### Camera Not Working
**Problem**: Black screen or error message
**Solutions**:
1. Check camera permissions in Settings
2. Restart the app
3. Restart the device
4. Check if camera works in other apps

### No Detection Results
**Problem**: "No car parts detected" message
**Solutions**:
1. Use better lighting
2. Take clearer photos
3. Ensure parts are visible
4. Check if model file exists

### App Crashes
**Problem**: App closes unexpectedly
**Solutions**:
1. Check device has Android 7.0+
2. Clear app cache
3. Reinstall the app
4. Check logcat for errors

### Slow Detection
**Problem**: Takes long time to process
**Solutions**:
1. Use smaller images
2. Close background apps
3. Check device has enough RAM
4. Consider using GPU acceleration

## FAQs

### Does this require internet?
No, all processing happens on-device.

### Is my data private?
Yes, no images or data leave your device.

### Which car parts can it detect?
See labels.txt for complete list. Default includes:
- Battery, Alternator, Engine Block
- Radiator, Air Filter, Oil Filter
- Spark Plugs, Fuel Injectors
- And more...

### Can I use my own AI model?
Yes! Place your .tflite model in assets folder.

### What Android version is required?
Android 7.0 (API 24) or higher.

### Does it work offline?
Yes, completely offline after installation.

### Can I detect multiple parts at once?
Yes, shows up to 5 detections per image.

## Getting Help

- 📖 **Documentation**: See README.md
- 🏗️ **Architecture**: See ARCHITECTURE.md
- 🔧 **Build Guide**: See BUILD_AND_TEST.md
- 🤝 **Contributing**: See CONTRIBUTING.md
- 🐛 **Issues**: GitHub Issues page

## Next Steps

### For Users
- Try detecting different car parts
- Experiment with various angles
- Compare confidence scores
- Share feedback on GitHub

### For Developers
- Train custom detection model
- Add new features (see CONTRIBUTING.md)
- Improve UI/UX
- Add tests
- Submit pull requests

## Resources

- [TensorFlow Lite](https://www.tensorflow.org/lite)
- [CameraX](https://developer.android.com/training/camerax)
- [Material Design](https://material.io/design)
- [Kotlin](https://kotlinlang.org/)

---

**Ready to start?** Download from Releases or build from source!

**Found a bug?** Report it on GitHub Issues.

**Have a feature idea?** Open a discussion on GitHub.

**Want to contribute?** Check CONTRIBUTING.md!
