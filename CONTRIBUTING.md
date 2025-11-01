# Contributing to AI Car Parts Detector

Thank you for your interest in contributing to the AI Car Parts Detector project! This document provides guidelines and information for contributors.

## Getting Started

1. **Fork the Repository**
   - Click the "Fork" button on GitHub
   - Clone your fork locally

2. **Set Up Development Environment**
   - Install Android Studio (latest stable version)
   - Install required SDKs (see BUILD_AND_TEST.md)
   - Open the project in Android Studio

3. **Create a Branch**
   - Create a feature branch: `git checkout -b feature/your-feature-name`
   - Or a bugfix branch: `git checkout -b fix/bug-description`

## Code Style

### Kotlin Code Style

Follow the [Kotlin Coding Conventions](https://kotlinlang.org/docs/coding-conventions.html):

- Use 4 spaces for indentation
- Class names: PascalCase
- Function names: camelCase
- Constants: UPPER_SNAKE_CASE
- Package names: lowercase

### XML Style

- Use 4 spaces for indentation
- Use self-closing tags when possible
- Order attributes: `id`, `layout_*`, `android:*`, `app:*`, `tools:*`
- Use descriptive IDs: `btnCapture`, `tvResults`, `viewFinder`

### File Organization

- One top-level class per file
- Related classes can be in the same file if small
- Organize imports (Android Studio can do this automatically)
- Remove unused imports

## Making Changes

### Before You Start

1. Check existing issues to avoid duplicate work
2. Create an issue to discuss major changes
3. Ensure your change aligns with project goals

### While Coding

1. Write clean, readable code
2. Add comments for complex logic
3. Follow existing patterns in the codebase
4. Keep changes focused and minimal

### Testing Your Changes

1. Test on multiple devices/emulators if possible
2. Test with and without TensorFlow model
3. Test camera capture and gallery selection
4. Verify UI looks correct on different screen sizes
5. Check logcat for errors or warnings

## Submitting Changes

### Commit Messages

Write clear, descriptive commit messages:

```
Good:
- "Add support for landscape orientation"
- "Fix crash when camera permission denied"
- "Improve detection confidence threshold"

Bad:
- "Update"
- "Fix bug"
- "Changes"
```

### Pull Request Process

1. **Update Documentation**
   - Update README.md if needed
   - Add comments to complex code
   - Update ARCHITECTURE.md for structural changes

2. **Create Pull Request**
   - Push your branch to your fork
   - Open a PR against the main repository
   - Provide a clear description of changes
   - Reference any related issues

3. **PR Description Should Include**
   - What problem does this solve?
   - How does this change solve it?
   - Any breaking changes?
   - Screenshots (for UI changes)
   - Testing steps

4. **Code Review**
   - Respond to feedback promptly
   - Make requested changes
   - Keep discussions professional and constructive

## Areas for Contribution

### High Priority

- [ ] Add real TensorFlow Lite model for car parts detection
- [ ] Implement bounding box visualization
- [ ] Add real-time detection during camera preview
- [ ] Improve error handling and user feedback
- [ ] Add unit and instrumented tests

### Medium Priority

- [ ] Support for multiple languages (i18n)
- [ ] Dark theme support
- [ ] Accessibility improvements
- [ ] Performance optimizations
- [ ] Better model management (download, update)

### Low Priority

- [ ] Export detection results
- [ ] Share detected images with results
- [ ] Detection history
- [ ] Part information database
- [ ] Settings screen

## Code Review Checklist

Before submitting, ensure:

- [ ] Code compiles without errors
- [ ] No new warnings introduced
- [ ] Code follows project style guidelines
- [ ] Changes are tested on a device/emulator
- [ ] No sensitive information (API keys, etc.) committed
- [ ] Documentation is updated
- [ ] Commit messages are clear
- [ ] PR description is complete

## Adding Dependencies

When adding new dependencies:

1. Explain why it's needed
2. Consider app size impact
3. Check license compatibility
4. Use latest stable version
5. Update build.gradle appropriately

## Working with TensorFlow Lite Models

If contributing a trained model:

1. Provide model training details
2. Include accuracy metrics
3. Document input/output format
4. Ensure model is optimized for mobile
5. Include sample images for testing
6. Update labels.txt accordingly

## Reporting Issues

When reporting bugs:

1. Check if issue already exists
2. Provide clear title and description
3. Include steps to reproduce
4. Specify Android version and device
5. Include relevant logs (logcat)
6. Add screenshots if applicable

## Questions?

- Open an issue for questions
- Tag with "question" label
- Be specific about what you need help with

## License

By contributing, you agree that your contributions will be licensed under the same license as the project (MIT License).

## Recognition

Contributors will be acknowledged in:
- README.md contributors section
- Release notes
- Project documentation

Thank you for contributing to AI Car Parts Detector!
