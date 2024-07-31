# Module 4: Cloud Firestore

## Lesson 2: Setting up Firestore in Flutter

### Adding Firestore Dependencies

Add Firestore dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  cloud_firestore: latest_version
```

### Initializing Firestore in Flutter

``` dart
import 'package:cloud_firestore/cloud_firestore.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}
```

### Verifying Firestore Initialization

Ensure that Firestore is correctly initialized by checking for any errors in the console during app startup.
