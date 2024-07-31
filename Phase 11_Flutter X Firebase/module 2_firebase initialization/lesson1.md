# Module 2: Firebase Initialization

## Lesson 1: Adding Firebase to Flutter Project

### Installing Necessary Dependencies

Add the required dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  firebase_core: latest_version
  firebase_auth: latest_version
  cloud_firestore: latest_version
  firebase_storage: latest_version
  ```

### Configuring Firebase in Android

1. Place the google-services.json file in the android/app directory.
2. Add the following to your `android/build.gradle` file:

```gradle
classpath 'com.google.gms:google-services:4.3.8'
```

Add the following to your `android/app/build.gradle` file:

```gradle
apply plugin: 'com.google.gms.google-services'
```

### Configuring Firebase in iOS

1. Place the `GoogleService-Info.plist` file in the `ios/Runner` directory.
2. Add the following in your `ios/Podfile`:

```ruby
platform :ios, '10.0'
```

Run `pod install` in the ios directory.
