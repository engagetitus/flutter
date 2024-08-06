# Module 7: State Management with MobX

## Lesson 2: Practical State Management - App Settings

In this lesson, we will create an app settings module that allows users to set font size, font family, theme, colors, and language. We will explore how to manage these settings using `MobX`.

### Setting Up the Project

Add the `flutter_mobx`, `mobx`, and `provider` dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_mobx: ^2.0.0
  mobx: ^2.0.0
  provider: ^6.0.0

dev_dependencies:
  build_runner: ^2.0.0
  mobx_codegen: ^2.0.0
```

### App Settings Model and MobX Setup

First, let's create the app settings model and MobX store.

#### Store

Create a file named `app_settings_store.dart`.

```dart
import 'package:mobx/mobx.dart';
import 'package:flutter/material.dart';

part 'app_settings_store.g.dart';

class AppSettingsStore = _AppSettingsStore with _$AppSettingsStore;

abstract class _AppSettingsStore with Store {
  // Theme settings
  @observable
  bool isDarkMode = false;

  @action
  void toggleTheme() {
    isDarkMode = !isDarkMode;
  }

  // Font size settings
  @observable
  double fontSize = 16.0;

  @action
  void setFontSize(double size) {
    fontSize = size;
  }

  // Font family settings
  @observable
  String fontFamily = 'Roboto';

  @action
  void setFontFamily(String family) {
    fontFamily = family;
  }

  // Primary color settings
  @observable
  Color primaryColor = Colors.blue;

  @action
  void setPrimaryColor(Color color) {
    primaryColor = color;
  }

  // Language settings
  @observable
  Locale locale = Locale('en');

  @action
  void setLocale(String languageCode) {
    locale = Locale(languageCode);
  }
}
```

Run the build_runner command to generate the necessary code:

```sh
flutter packages pub run build_runner build
```

### Integrating MobX

Next, integrate the `AppSettingsStore` with the Flutter app.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_mobx/flutter_mobx.dart';
import 'package:provider/provider.dart';
import 'app_settings_store.dart';

void main() {
  runApp(
    Provider<AppSettingsStore>(
      create: (_) => AppSettingsStore(),
      child: MyApp(),
    ),
  );
}

// Main application widget
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final appSettings = Provider.of<AppSettingsStore>(context);

    return Observer(
      builder: (_) {
        return MaterialApp(
          theme: appSettings.isDarkMode ? ThemeData.dark() : ThemeData.light(),
          locale: appSettings.locale,
          home: HomeScreen(),
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
import 'package:flutter_mobx/flutter_mobx.dart';
import 'package:provider/provider.dart';
import 'app_settings_store.dart';

// Settings screen where users can adjust app settings
class SettingsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final appSettings = Provider.of<AppSettingsStore>(context);

    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Observer(
          builder: (_) {
            return ListView(
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
            );
          },
        ),
      ),
    );
  }
}
```

### Applying Settings to the App

Modify the main app to apply the settings from `AppSettingsStore`.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final appSettings = Provider.of<AppSettingsStore>(context);

    return Observer(
      builder: (_) {
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
```

### Complete Code

Here’s the complete code for the app with comments:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_mobx/flutter_mobx.dart';
import 'package:mobx/mobx.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    Provider<AppSettingsStore>(
      create: (_) => AppSettingsStore(),
      child: MyApp(),
    ),
  );
}

// AppSettingsStore
part 'app_settings_store.g.dart';

class AppSettingsStore = _AppSettingsStore with _$AppSettingsStore;

abstract class _AppSettingsStore with Store {
  // Theme settings
  @observable
  bool isDarkMode = false;

  @action
  void toggleTheme() {
    isDarkMode = !isDarkMode;
  }

  // Font size settings
  @observable
  double fontSize = 16.0;

  @action
  void setFontSize(double size) {
    fontSize = size;
  }

  // Font family settings
  @observable
  String fontFamily = 'Roboto';

  @action
  void setFontFamily(String family) {
    fontFamily = family;
  }

  // Primary color settings
  @observable
  Color primaryColor = Colors.blue;

  @action
  void setPrimaryColor(Color color) {
    primaryColor = color;
  }

  // Language settings
  @observable
  Locale locale = Locale('en');

  @action
  void setLocale(String languageCode) {
    locale = Locale(languageCode);
  }
}

// Main application widget
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final appSettings = Provider.of<AppSettingsStore>(context);

    return Observer(
      builder: (_) {
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
      },
    );
  }
}

// Home screen of the app
class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return

 Scaffold(
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
class SettingsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final appSettings = Provider.of<AppSettingsStore>(context);

    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Observer(
          builder: (_) {
            return ListView(
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
            );
          },
        ),
      ),
    );
  }
}
```
