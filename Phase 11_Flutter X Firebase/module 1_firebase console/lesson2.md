# Module 1: Firebase Console

## Lesson 2: Setting up Firebase Project

### Creating a Firebase Project

1. Go to the [Firebase Console](https://console.firebase.google.com/).
2. Click on "Add project".
3. Enter your project name and configure Google Analytics if needed.
4. Click "Create project".

### Configuring Project Settings

1. Navigate to the Project Settings.
2. Add your app (iOS, Android, Web) to the Firebase project.
3. Download the `google-services.json` (for Android) or `GoogleService-Info.plist` (for iOS) file.

### Adding Firebase to Your Flutter App

1. Add Firebase SDK dependencies in your `pubspec.yaml` file:

   ```yaml
   dependencies:
     firebase_core: latest_version
     firebase_auth: latest_version
    ```

2. Run flutter pub get to install the dependencies.
3. Initialize Firebase in your app:

```dart
import 'package:firebase_core/firebase_core.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}


```
