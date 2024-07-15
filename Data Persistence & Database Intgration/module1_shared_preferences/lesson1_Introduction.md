
# Introduction to Shared Preferences

## Purpose
Shared Preferences are used to store simple data persistently in Flutter applications, such as user settings or small amounts of data that need to be retained across app sessions.

## Key Concepts
- **Key-Value Storage:** Data is stored in key-value pairs.
- **SharedPreferences Class:** Provides methods to save and retrieve data.

## Installation
To use Shared Preferences in a Flutter app, you need to add the `shared_preferences` package to your `pubspec.yaml` file.

```yaml
dependencies:
  shared_preferences: ^2.0.6
```

Then, run `flutter pub get` to install the package.

## Initialization
Before using Shared Preferences, you need to initialize an instance of the `SharedPreferences` class.

```dart
import 'package:shared_preferences/shared_preferences.dart';

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  SharedPreferences prefs = await SharedPreferences.getInstance();
  runApp(MyApp(prefs: prefs));
}
```
