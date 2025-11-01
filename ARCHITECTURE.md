# Application Architecture

## Overview

The AI Car Parts Detector follows a simple, activity-based architecture suitable for a focused, single-purpose application.

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────┐
│                     MainActivity                         │
│  ┌───────────────────────────────────────────────────┐  │
│  │           UI Layer (XML Layouts)                   │  │
│  │  - Camera Preview (PreviewView)                    │  │
│  │  - Image Preview (ImageView)                       │  │
│  │  - Action Buttons (Capture, Select)                │  │
│  │  - Results Display (ScrollView + TextView)         │  │
│  │  - Progress Indicator (ProgressBar)                │  │
│  └───────────────────────────────────────────────────┘  │
│                          │                               │
│                          ▼                               │
│  ┌───────────────────────────────────────────────────┐  │
│  │        Business Logic Layer (Kotlin)               │  │
│  │  - Camera Management (CameraX)                     │  │
│  │  - Image Capture & Selection                       │  │
│  │  - Permission Handling                             │  │
│  │  - UI State Management                             │  │
│  └───────────────────────────────────────────────────┘  │
│                          │                               │
│                          ▼                               │
│  ┌───────────────────────────────────────────────────┐  │
│  │          CarPartsDetector                          │  │
│  │  - TensorFlow Lite Integration                     │  │
│  │  - Image Preprocessing                             │  │
│  │  - Model Inference                                 │  │
│  │  - Result Processing                               │  │
│  └───────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│                  External Dependencies                   │
│  - CameraX (Camera abstraction)                         │
│  - TensorFlow Lite (AI inference)                       │
│  - Material Components (UI)                             │
└─────────────────────────────────────────────────────────┘
```

## Components

### 1. MainActivity (`MainActivity.kt`)

**Responsibilities:**
- Manages the application lifecycle
- Handles camera preview and image capture
- Coordinates image selection from gallery
- Manages permissions (camera, storage)
- Updates UI based on detection results
- Handles background threading for image processing

**Key Methods:**
- `startCamera()`: Initializes CameraX and binds camera preview
- `takePhoto()`: Captures image from camera
- `selectImageFromGallery()`: Opens gallery for image selection
- `processImage()`: Sends image to CarPartsDetector for inference
- `displayResults()`: Shows detection results in UI

**Threading:**
- UI operations: Main thread
- Image processing & AI inference: Background executor
- Camera operations: CameraX executor

### 2. CarPartsDetector (`CarPartsDetector.kt`)

**Responsibilities:**
- Loads and manages TensorFlow Lite model
- Preprocesses images for model input
- Runs inference on images
- Post-processes results
- Manages model lifecycle

**Key Methods:**
- `loadModelAndLabels()`: Initializes TensorFlow Lite interpreter
- `detectParts()`: Performs car parts detection on bitmap
- `getMockDetections()`: Provides demo results when model is unavailable
- `close()`: Cleans up resources

**Image Processing Pipeline:**
1. Convert Bitmap to TensorImage
2. Resize to model input size (224x224)
3. Normalize pixel values
4. Run inference
5. Extract top N results above confidence threshold
6. Map indices to labels

### 3. UI Layer (`activity_main.xml`)

**Components:**
- **PreviewView**: Real-time camera preview using CameraX
- **ImageView**: Displays captured or selected image
- **MaterialButton** (Take Photo): Triggers camera capture
- **MaterialButton** (Select Image): Opens gallery picker
- **ScrollView**: Container for detection results
- **TextView**: Displays detection results with confidence scores
- **ProgressBar**: Shows loading state during processing

**Layout Structure:**
```
ConstraintLayout
├── PreviewView (camera preview)
├── ImageView (image display)
├── LinearLayout (button container)
│   ├── MaterialButton (select image)
│   └── MaterialButton (take photo)
├── ScrollView (results container)
│   └── LinearLayout
│       ├── TextView (results title)
│       └── TextView (results content)
└── ProgressBar (loading indicator)
```

## Data Flow

### Image Capture Flow
```
User Taps "TAKE PHOTO"
    ↓
MainActivity.takePhoto()
    ↓
CameraX captures image
    ↓
Image saved to file
    ↓
MainActivity.displayImage()
    ↓
MainActivity.processImage()
    ↓
CarPartsDetector.detectParts()
    ↓
TensorFlow Lite inference
    ↓
MainActivity.displayResults()
    ↓
UI updated with results
```

### Gallery Selection Flow
```
User Taps "SELECT IMAGE"
    ↓
MainActivity.selectImageFromGallery()
    ↓
System gallery opens
    ↓
User selects image
    ↓
MainActivity receives URI
    ↓
MainActivity.displayImage()
    ↓
MainActivity.processImage()
    ↓
CarPartsDetector.detectParts()
    ↓
TensorFlow Lite inference
    ↓
MainActivity.displayResults()
    ↓
UI updated with results
```

## Key Technologies

### CameraX
- Modern camera API for Android
- Handles compatibility across devices
- Provides lifecycle-aware camera management
- Supports image capture and preview

### TensorFlow Lite
- Optimized for mobile inference
- Runs models on-device (no server required)
- Support for hardware acceleration (GPU, NNAPI)
- Small binary size suitable for mobile apps

### Material Components
- Modern UI components following Material Design
- Consistent look and feel across Android versions
- Built-in support for theming and accessibility

## Threading Model

The app uses multiple threads to maintain responsiveness:

1. **Main Thread (UI Thread)**
   - All UI updates
   - Event handling (button clicks)
   - Lifecycle callbacks

2. **CameraX Executor**
   - Camera operations
   - Image capture callbacks
   - Managed by CameraX internally

3. **Background Executor (Single Thread)**
   - Image loading and preprocessing
   - TensorFlow Lite inference
   - Result post-processing

## Error Handling

The app handles several error scenarios:

1. **Camera Permission Denied**: Shows toast message
2. **Camera Initialization Failed**: Logs error and shows toast
3. **Image Processing Failed**: Logs error and shows toast
4. **Model Not Found**: Falls back to mock detections
5. **Labels File Missing**: Uses default labels

## Future Enhancements

Potential improvements to the architecture:

1. **MVVM Pattern**: Introduce ViewModel for better state management
2. **Repository Pattern**: Abstract data sources
3. **Dependency Injection**: Use Hilt/Dagger for better testability
4. **Coroutines**: Replace executors with Kotlin coroutines
5. **Room Database**: Cache detection results
6. **WorkManager**: Background processing for batch images
7. **Custom Views**: Bounding box overlay for detected parts
