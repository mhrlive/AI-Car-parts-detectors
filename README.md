# AI Car Parts Detector

An Android application built with Kotlin and XML that uses camera photos and AI to detect car engine parts.

## Features

- 📷 **Camera Integration**: Capture photos directly from the app using CameraX
- 🖼️ **Gallery Support**: Select images from your device gallery
- 🤖 **AI Detection**: Uses TensorFlow Lite for car parts detection
- 📊 **Confidence Scores**: Displays detection results with confidence percentages
- 🎨 **Modern UI**: Clean Material Design interface

## Screenshots

The app provides a camera preview with buttons to capture or select images, and displays detection results with confidence scores.

## Technical Stack

- **Language**: Kotlin
- **UI**: XML Layouts with Material Components
- **Camera**: AndroidX CameraX
- **AI Framework**: TensorFlow Lite
- **Architecture**: Activity-based with ViewBinding
- **Minimum SDK**: 24 (Android 7.0)
- **Target SDK**: 34 (Android 14)

## Detected Car Parts

The app can detect various car engine parts including:
- Engine Block
- Battery
- Radiator
- Alternator
- Air Filter
- Spark Plug
- Fuel Injector
- Timing Belt
- Water Pump
- Oil Filter
- And more...

## How to Build

### Prerequisites
- Android Studio Hedgehog or later
- JDK 8 or higher
- Android SDK with API level 34

### Build Steps

1. Clone the repository:
```bash
git clone https://github.com/mhrlive/AI-Car-parts-detectors.git
cd AI-Car-parts-detectors
```

2. Open the project in Android Studio

3. Sync Gradle files

4. Build and run on an emulator or physical device

## How to Use

1. **Launch the app** - The camera preview will appear
2. **Take a photo** - Tap the "TAKE PHOTO" button to capture an image
3. **Or select an image** - Tap "SELECT IMAGE" to choose from gallery
4. **View results** - Detection results appear at the bottom with confidence scores

## Adding Your Own AI Model

The app supports custom TensorFlow Lite models:

1. Train your model to detect car parts
2. Convert it to `.tflite` format
3. Place it in `app/src/main/assets/car_parts_model.tflite`
4. Update `app/src/main/assets/labels.txt` with your class labels

If no model is provided, the app uses mock detections for demonstration purposes.

## Permissions

The app requires the following permissions:
- **Camera**: To capture photos
- **Read External Storage**: To select images from gallery (API < 33)

## Project Structure

```
app/
├── src/main/
│   ├── java/com/carparts/detector/
│   │   ├── MainActivity.kt          # Main activity with camera & UI logic
│   │   └── CarPartsDetector.kt      # TensorFlow Lite inference
│   ├── res/
│   │   ├── layout/
│   │   │   └── activity_main.xml    # Main UI layout
│   │   ├── values/
│   │   │   ├── strings.xml          # String resources
│   │   │   ├── colors.xml           # Color definitions
│   │   │   └── themes.xml           # App theme
│   │   └── drawable/                # Icons and drawables
│   ├── assets/
│   │   └── labels.txt               # Car parts labels
│   └── AndroidManifest.xml          # App manifest
```

## Dependencies

- AndroidX Core KTX
- AndroidX AppCompat
- Material Components
- ConstraintLayout
- CameraX (Core, Camera2, Lifecycle, View)
- TensorFlow Lite (Core, Support, GPU)
- ExifInterface

## License

This project is open source and available under the MIT License.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Future Enhancements

- [ ] Real-time detection while camera is active
- [ ] Bounding box visualization on detected parts
- [ ] Multi-language support
- [ ] Part identification with detailed information
- [ ] AR overlay for real-time part labels
- [ ] Export detection results

## Author

Created for car enthusiasts and mechanics to easily identify engine parts.
