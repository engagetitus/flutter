# Module 3: State Management with Riverpod

## Lesson 2: Practical State Management - App Settings

In this lesson, we will create an app settings module that allows users to set font size, font family, theme, colors, and language. We will explore how to manage these settings using `Riverpod`.

### Setting Up the Project

Add the `flutter_riverpod` dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_riverpod: ^1.0.0
```

### App Settings Model

First, let's create a model to manage the app settings.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

// Provider to manage app settings
class AppSettings extends ChangeNotifier {
  // Theme settings
  bool _isDarkMode = false;
  bool get isDarkMode => _isDarkMode;

  void toggleTheme() {
    _isDarkMode = !_isDarkMode;
    notifyListeners();
  }

  // Font size settings
  double _fontSize = 16.0;
  double get fontSize => _fontSize;

  void setFontSize(double size) {
    _fontSize = size;
    notifyListeners();
  }

  // Font family settings
  String _fontFamily = 'Roboto';
  String get fontFamily => _fontFamily;

  void setFontFamily(String family) {
    _fontFamily = family;
    notifyListeners();
  }

  // Primary color settings
  Color _primaryColor = Colors.blue;
  Color get primaryColor => _primaryColor;

  void setPrimaryColor(Color color) {
    _primaryColor = color;
    notifyListeners();
  }

  // Language settings
  Locale _locale = Locale('en');
  Locale get locale => _locale;

  void setLocale(String languageCode) {
    _locale = Locale(languageCode);
    notifyListeners();
  }
}

// Global provider for AppSettings
final appSettingsProvider = ChangeNotifierProvider((ref) => AppSettings());
```

### Integrating Riverpod

Next, integrate the `AppSettings` model with `Riverpod`.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

void main() {
  runApp(
    ProviderScope(
      child: MyApp(),
    ),
  );
}

// Main application widget
class MyApp extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final appSettings = ref.watch(appSettingsProvider);

    return MaterialApp(
      theme: appSettings.isDarkMode ? ThemeData.dark() : ThemeData.light(),
      locale: appSettings.locale,
      home: HomeScreen(),
    );
  }
}
```

### Creating the Settings Screen

Create a settings screen where users can adjust the app settings.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'app_settings_model.dart';

// Settings screen where users can adjust app settings
class SettingsScreen extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final appSettings = ref.watch(appSettingsProvider);

    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: ListView(
          children: [
            // Toggle for dark mode
            ListTile(
              title: Text('Dark Mode'),
              trailing: Switch(
                value: appSettings.isDarkMode,
                onChanged: (value) {
                  appSettings.toggleTheme();
                },
              ),
            ),
            // Slider for font size
            ListTile(
              title: Text('Font Size'),
              subtitle: Slider(
                min: 10,
                max: 30,
                value: appSettings.fontSize,
                onChanged: (value) {
                  appSettings.setFontSize(value);
                },
              ),
            ),
            // Dropdown for font family
            ListTile(
              title: Text('Font Family'),
              subtitle: DropdownButton<String>(
                value: appSettings.fontFamily,
                items: ['Roboto', 'Arial', 'Times New Roman'].map((String value) {
                  return DropdownMenuItem<String>(
                    value: value,
                    child: Text(value),
                  );
                }).toList(),
                onChanged: (value) {
                  appSettings.setFontFamily(value!);
                },
              ),
            ),
            // Color picker for primary color
            ListTile(
              title: Text('Primary Color'),
              subtitle: Row(
                children: Colors.primaries.map((color) {
                  return GestureDetector(
                    onTap: () {
                      appSettings.setPrimaryColor(color);
                    },
                    child: Container(
                      margin: EdgeInsets.symmetric(horizontal: 5),
                      width: 30,
                      height: 30,
                      color: color,
                    ),
                  );
                }).toList(),
              ),
            ),
            // Dropdown for language selection
            ListTile(
              title: Text('Language'),
              subtitle: DropdownButton<Locale>(
                value: appSettings.locale,
                items: [
                  Locale('en', 'English'),
                  Locale('es', 'Spanish'),
                ].map((Locale value) {
                  return DropdownMenuItem<Locale>(
                    value: value,
                    child: Text(value.languageCode),
                  );
                }).toList(),
                onChanged: (value) {
                  appSettings.setLocale(value!.languageCode);
                },
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

### Applying Settings to the App

Modify the main app to apply the settings from `AppSettings`.

```dart
class MyApp extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final appSettings = ref.watch(appSettingsProvider);

    return MaterialApp(
      theme: ThemeData(
        brightness: appSettings.isDarkMode ? Brightness.dark : Brightness.light,
        primaryColor: appSettings.primaryColor,
        textTheme: TextTheme(
          bodyText2: TextStyle(
            fontSize: appSettings.fontSize,
            fontFamily: appSettings.fontFamily,
          ),
        ),
      ),
      locale: appSettings.locale,
      home: HomeScreen(),
    );
  }
}

// Home screen of the app
class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(child: Text('Welcome to the App')),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          Navigator.of(context).push(MaterialPageRoute(builder: (context) => SettingsScreen()));
        },
        child: Icon(Icons.settings),
      ),
    );
  }
}
```

### Complete Code

Here’s the complete code for the app with comments:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

void main() {
  runApp(
    ProviderScope(
      child: MyApp(),
    ),
  );
}

// Provider to manage app settings
class AppSettings extends ChangeNotifier {
  // Theme settings
  bool _isDarkMode = false;
  bool get isDarkMode => _isDarkMode;

  void toggleTheme() {
    _isDarkMode = !_isDarkMode;
    notifyListeners();
  }

  // Font size settings
  double _fontSize = 16.0;
  double get fontSize => _fontSize;

  void setFontSize(double size) {
    _fontSize = size;
    notifyListeners();
  }

  // Font family settings
  String _fontFamily = 'Roboto';
  String get fontFamily => _fontFamily;

  void setFontFamily(String family) {
    _fontFamily = family;
    notifyListeners();
  }

  // Primary color settings
  Color _primaryColor = Colors.blue;
  Color get primaryColor => _primaryColor;

  void setPrimaryColor(Color color) {
    _primaryColor = color;
    notifyListeners();
  }

  // Language settings
  Locale _locale = Locale('en');
  Locale get locale => _locale;

  void setLocale(String languageCode) {
    _locale = Locale(languageCode);
    notifyListeners();
  }
}

// Global provider for AppSettings
final appSettingsProvider = ChangeNotifierProvider((ref) => AppSettings());

// Main application widget
class MyApp extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // Watch the appSettingsProvider to get the current settings
    final appSettings = ref.watch(appSettingsProvider);

    return MaterialApp(
      // Apply theme settings
      theme: ThemeData(
        brightness: appSettings.isDarkMode ? Brightness.dark : Brightness.light,
        primaryColor: appSettings.primaryColor,
        textTheme: TextTheme(
          bodyText2: TextStyle(
            fontSize: appSettings.fontSize,
            fontFamily: appSettings.fontFamily,
          ),
        ),
      ),
      // Apply locale settings
      locale: appSettings.locale,
      home: HomeScreen(),
    );
  }
}

// Home screen of the app
class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(child: Text('Welcome to the App')),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Navigate to the Settings screen
          Navigator.of(context).push(MaterialPageRoute(builder: (context) => SettingsScreen()));
        },
        child: Icon(Icons.settings),
      ),
    );
  }
}

// Settings screen where users can adjust app settings
class SettingsScreen extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // Watch

 the appSettingsProvider to get the current settings
    final appSettings = ref.watch(appSettingsProvider);

    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: ListView(
          children: [
            // Toggle for dark mode
            ListTile(
              title: Text('Dark Mode'),
              trailing: Switch(
                value: appSettings.isDarkMode,
                onChanged: (value) {
                  appSettings.toggleTheme();
                },
              ),
            ),
            // Slider for font size
            ListTile(
              title: Text('Font Size'),
              subtitle: Slider(
                min: 10,
                max: 30,
                value: appSettings.fontSize,
                onChanged: (value) {
                  appSettings.setFontSize(value);
                },
              ),
            ),
            // Dropdown for font family
            ListTile(
              title: Text('Font Family'),
              subtitle: DropdownButton<String>(
                value: appSettings.fontFamily,
                items: ['Roboto', 'Arial', 'Times New Roman'].map((String value) {
                  return DropdownMenuItem<String>(
                    value: value,
                    child: Text(value),
                  );
                }).toList(),
                onChanged: (value) {
                  appSettings.setFontFamily(value!);
                },
              ),
            ),
            // Color picker for primary color
            ListTile(
              title: Text('Primary Color'),
              subtitle: Row(
                children: Colors.primaries.map((color) {
                  return GestureDetector(
                    onTap: () {
                      appSettings.setPrimaryColor(color);
                    },
                    child: Container(
                      margin: EdgeInsets.symmetric(horizontal: 5),
                      width: 30,
                      height: 30,
                      color: color,
                    ),
                  );
                }).toList(),
              ),
            ),
            // Dropdown for language selection
            ListTile(
              title: Text('Language'),
              subtitle: DropdownButton<Locale>(
                value: appSettings.locale,
                items: [
                  Locale('en', 'English'),
                  Locale('es', 'Spanish'),
                ].map((Locale value) {
                  return DropdownMenuItem<Locale>(
                    value: value,
                    child: Text(value.languageCode),
                  );
                }).toList(),
                onChanged: (value) {
                  appSettings.setLocale(value!.languageCode);
                },
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```
