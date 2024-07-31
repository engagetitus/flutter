
# Module 2: Firebase Initialization

## Lesson 2: Initializing Firebase in Flutter

### Setting up Firebase Initialization Code

Initialize Firebase in your `main.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Firebase Initialization')),
        body: Center(child: Text('Firebase is initialized')),
      ),
    );
  }
}
```

- Ensuring Proper Firebase Setup in `main.dart`
- Ensure that Firebase initialization is completed before running the app:

```dart

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}
```

### Testing Firebase Initialization

Run the app and check the console for any initialization errors. Verify Firebase is initialized correctly:

**Android**: Check Logcat for any errors.
**iOS**: Check Xcode console for errors.
