# Module 7: Cloud Messaging

## Lesson 2: Setting up Cloud Messaging

Setting up Firebase Cloud Messaging involves adding necessary dependencies and configuring it in the Firebase Console.

### Adding Cloud Messaging Dependencies

Include the FCM plugin in your Flutter project by adding it to your `pubspec.yaml` file:



```yaml
dependencies:
  firebase_messaging: latest_version
```

### Configuring Firebase Messaging 
Navigate to Firebase Console -> Project settings -> Cloud Messaging.
Add your app and configure it by uploading your APNs credentials for iOS or setting up your Android app with the server key.

### in Android

Add the `google-services.json` file in the `android/app` directory.
Configure the `build.gradle` files as instructed in the Firebase Console.

### in iOS



Add the `GoogleService-Info.plist` file in the `ios/Runner` directory.
Configure the `AppDelegate.swift` file to handle notifications.
