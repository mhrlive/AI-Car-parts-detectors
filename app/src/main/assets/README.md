# AI Car Parts Detector - Assets

This directory contains the AI model and labels for car parts detection.

## Files:
- `labels.txt`: Contains the list of car engine parts that can be detected
- `car_parts_model.tflite`: TensorFlow Lite model for car parts detection (optional)

## Using Your Own Model:

To use a custom TensorFlow Lite model:
1. Train your model to detect car engine parts
2. Convert it to TensorFlow Lite format (.tflite)
3. Place the model file in this directory as `car_parts_model.tflite`
4. Update `labels.txt` with your model's class labels

The app will automatically use the model if present, otherwise it will use mock detections for demonstration purposes.
