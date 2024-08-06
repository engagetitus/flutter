# Module 2: Provider for State Management

## Lesson 4: Practical State Management - App Settings

In this lesson, we will create an app settings module that allows users to set font size, font family, theme, colors, and language. We will explore how to manage these settings using `ChangeNotifier` with `Provider`.

### Setting Up the Project

Add the `provider` dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  provider: ^6.0.0
```

### App Settings Model

First, let's create a model to manage the app settings.

```dart
import 'package:flutter/material.dart';

class AppSettings with ChangeNotifier {
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
```

### Integrating Provider

Next, integrate the `AppSettings` model with `Provider`.

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => AppSettings(),
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<AppSettings>(
      builder: (context, appSettings, child) {
        return MaterialApp(
          theme: appSettings.isDarkMode ? ThemeData.dark() : ThemeData.light(),
          locale: appSettings.locale,
          home: SettingsScreen(),
        );
      },
    );
  }
}
```

### Creating the Settings Screen

Create a settings screen where users can adjust the app settings.

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

class SettingsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final appSettings = Provider.of<AppSettings>(context);

    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: ListView(
          children: [
            // Theme toggle
            ListTile(
              title: Text('Dark Mode'),
              trailing: Switch(
                value: appSettings.isDarkMode,
                onChanged: (value) {
                  appSettings.toggleTheme();
                },
              ),
            ),
            // Font size slider
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
            // Font family dropdown
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
            // Primary color picker
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
            // Language dropdown
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
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<AppSettings>(
      builder: (context, appSettings, child) {
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
      },
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(child: Text('Welcome to the App')),
    );
  }
}
```

### Complete Code

Here’s the complete code for the app:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

// AppSettings Model
class AppSettings with ChangeNotifier {
  bool _isDarkMode = false;
  bool get isDarkMode => _isDarkMode;

  void toggleTheme() {
    _isDarkMode = !_isDarkMode;
    notifyListeners();
  }

  double _fontSize = 16.0;
  double get fontSize => _fontSize;

  void setFontSize(double size) {
    _fontSize = size;
    notifyListeners();
  }

  String _fontFamily = 'Roboto';
  String get fontFamily => _fontFamily;

  void setFontFamily(String family) {
    _fontFamily = family;
    notifyListeners();
  }

  Color _primaryColor = Colors.blue;
  Color get primaryColor => _primaryColor;

  void setPrimaryColor(Color color) {
    _primaryColor = color;
    notifyListeners();
  }

  Locale _locale = Locale('en');
  Locale get locale => _locale;

  void setLocale(String languageCode) {
    _locale = Locale(languageCode);
    notifyListeners();
  }
}

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => AppSettings(),
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<AppSettings>(
      builder: (context, appSettings, child) {
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
      },
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(child: Text('Welcome to the App')),
    );
  }
}

class SettingsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final appSettings = Provider.of<AppSettings>(context);

    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: ListView(
          children: [
            ListTile(
              title: Text('Dark Mode'),
              trailing: Switch(
                value: appSettings.isDarkMode,
                onChanged: (value) {
                  appSettings.toggleTheme();
                },
              ),
            ),
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
