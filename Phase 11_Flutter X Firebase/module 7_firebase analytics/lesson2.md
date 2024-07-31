# Module 8: Firebase Analytics

## Lesson 2: Setting up Firebase Analytics

### Adding Analytics Dependencies

Add the required dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  firebase_analytics: latest_version
  ```

### Initializing Firebase Analytics

```dart

import 'package:firebase_analytics/firebase_analytics.dart';

FirebaseAnalytics analytics = FirebaseAnalytics.instance;

void main() {
  runApp(MyApp());
  analytics.logAppOpen();
}
```

### Configuring Firebase Analytics in Android

Add the `google-services.json` file in the `android/app` directory.
Configure the `build.gradle` files as instructed in the Firebase Console.

### Configuring Firebase Analytics in iOS

Add the `GoogleService-Info.plist` file in the `ios/Runner` directory.
Configure the `AppDelegate.swift` file to handle analytics.
