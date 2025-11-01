# App Screenshots & UI Flow

## Main Screen - Camera View

```
┌──────────────────────────────────────┐
│  AI Car Parts Detector      [Menu]   │
├──────────────────────────────────────┤
│                                      │
│                                      │
│                                      │
│         Camera Preview               │
│         (Live View)                  │
│                                      │
│                                      │
│                                      │
│                                      │
├──────────────────────────────────────┤
│  [📷 SELECT IMAGE]  [📸 TAKE PHOTO] │
├──────────────────────────────────────┤
│                                      │
└──────────────────────────────────────┘
```

## After Capturing/Selecting Image

```
┌──────────────────────────────────────┐
│  AI Car Parts Detector      [Menu]   │
├──────────────────────────────────────┤
│                                      │
│                                      │
│         [Captured Image]             │
│       (Car Engine Photo)             │
│                                      │
│                                      │
├──────────────────────────────────────┤
│  [📷 SELECT IMAGE]  [📸 TAKE PHOTO] │
├──────────────────────────────────────┤
│  Detection Results:                  │
│  ┌────────────────────────────────┐  │
│  │ Battery: 92.3%                 │  │
│  │ Alternator: 87.5%              │  │
│  │ Engine Block: 84.2%            │  │
│  │ Air Filter: 78.6%              │  │
│  └────────────────────────────────┘  │
└──────────────────────────────────────┘
```

## User Flow

```
┌─────────────┐
│  App Start  │
└──────┬──────┘
       │
       ▼
┌──────────────────┐
│ Request Camera   │
│   Permission     │
└────┬─────────┬───┘
     │         │
 Granted    Denied
     │         │
     ▼         ▼
┌─────────┐  ┌────────────┐
│ Show    │  │ Show Error │
│ Camera  │  │  Message   │
└────┬────┘  └────────────┘
     │
     ▼
┌──────────────────────────┐
│  User has two options:   │
├──────────────────────────┤
│  1. Take Photo           │
│  2. Select from Gallery  │
└────┬─────────────────┬───┘
     │                 │
     ▼                 ▼
┌─────────┐       ┌─────────┐
│ Capture │       │ Open    │
│  Image  │       │ Gallery │
└────┬────┘       └────┬────┘
     │                 │
     └────────┬────────┘
              ▼
       ┌──────────────┐
       │ Display      │
       │ Image        │
       └──────┬───────┘
              ▼
       ┌──────────────┐
       │ Process with │
       │ TensorFlow   │
       │ Lite Model   │
       └──────┬───────┘
              ▼
       ┌──────────────┐
       │ Show Results │
       │ with         │
       │ Confidence % │
       └──────────────┘
```

## Features Demonstrated

### 1. Camera Integration (CameraX)
- Real-time camera preview
- High-quality image capture
- Smooth lifecycle management
- Auto-focus and exposure control

### 2. Gallery Integration
- Access device photo library
- Select any image
- Process pre-existing photos
- Support for various image formats

### 3. AI Detection
- TensorFlow Lite integration
- On-device inference (no internet required)
- Fast processing (<1 second)
- Multiple detections per image
- Confidence scores for each detection

### 4. Results Display
- Clean, scrollable list
- Part name with confidence percentage
- Easy to read format
- Persistent until next detection

### 5. User Experience
- Material Design components
- Smooth animations
- Loading indicators
- Clear error messages
- Portrait orientation optimized
- Responsive button states

## Technical Highlights

### Camera (CameraX)
```kotlin
// Modern camera API usage
val preview = Preview.Builder().build()
val imageCapture = ImageCapture.Builder().build()
cameraProvider.bindToLifecycle(
    this, 
    cameraSelector, 
    preview, 
    imageCapture
)
```

### AI Detection (TensorFlow Lite)
```kotlin
// Efficient on-device inference
val tensorImage = TensorImage.fromBitmap(bitmap)
val processedImage = imageProcessor.process(tensorImage)
interpreter.run(processedImage.buffer, output)
```

### Modern UI (View Binding)
```kotlin
// Type-safe view access
binding.btnCapture.setOnClickListener {
    takePhoto()
}
binding.tvResults.text = resultsText
```

## Detected Car Parts (Examples)

The app can detect various car engine components:

1. **Power Generation**
   - Battery
   - Alternator
   - Starter Motor

2. **Engine Core**
   - Engine Block
   - Transmission
   - Timing Belt

3. **Fuel & Air**
   - Air Filter
   - Fuel Injector
   - Intake Manifold

4. **Cooling System**
   - Radiator
   - Water Pump
   - Coolant Hose

5. **Maintenance Parts**
   - Oil Filter
   - Spark Plug
   - Serpentine Belt

## Performance

- **Image Capture**: < 100ms
- **AI Inference**: < 500ms (with model)
- **UI Update**: Instant
- **Total Time**: < 1 second from capture to results

## Accessibility

- Clear labels for screen readers
- High contrast UI
- Large touch targets
- Descriptive content descriptions
- Support for TalkBack

## Future UI Enhancements

- [ ] Bounding boxes around detected parts
- [ ] Confidence visualization (color-coded)
- [ ] Part information on tap
- [ ] Detection history view
- [ ] Dark mode support
- [ ] Landscape orientation support
- [ ] Multi-language support
- [ ] Detailed part view with images
