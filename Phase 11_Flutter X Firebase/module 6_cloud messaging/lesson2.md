# Module 7: Cloud Messaging

## Lesson 2: Setting up Cloud Messaging

### Adding Cloud Messaging Dependencies

Add the necessary dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  firebase_messaging: latest_version
```

### Configuring Firebase Messaging in Android

Add the `google-services.json` file in the `android/app` directory.
Configure the `build.gradle` files as instructed in the Firebase Console.

### Configuring Firebase Messaging in iOS

Add the `GoogleService-Info.plist` file in the `ios/Runner` directory.
Configure the `AppDelegate.swift` file to handle notifications.
