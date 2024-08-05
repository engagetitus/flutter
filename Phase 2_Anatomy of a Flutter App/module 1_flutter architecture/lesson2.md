# Lesson 2: Understanding the Flutter Engine

- **Overview**: Detailed explanation of the Flutter engine.
- **Key Concepts**:
  - Skia Graphics Engine 🎨
  - Dart Virtual Machine (Dart VM) 🚀
  - Platform Channels for Native Code Communication 🔗

## Skia Graphics Engine 🎨

- Flutter uses the Skia graphics engine, which provides hardware-accelerated graphics. This makes Flutter apps performant and smooth.

## Dart Virtual Machine (Dart VM) 🚀

- The Dart VM executes Dart code and provides a rich set of libraries and runtime support for developing Flutter applications.

## Platform Channels for Native Code Communication 🔗

- Flutter uses platform channels to communicate with native code. This allows Flutter to interact with platform-specific APIs.

  ```dart
  // Example of a platform channel
  static const platform = MethodChannel('com.example/native');

  Future<void> _getBatteryLevel() async {
    try {
      final int result = await platform.invokeMethod('getBatteryLevel');
      print('Battery level: $result%');
    } on PlatformException catch (e) {
      print("Failed to get battery level: '${e.message}'.");
    }
  }

  ```
