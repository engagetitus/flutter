# Module 6: State Management with GetX

## Lesson 2: Practical State Management - App Settings

In this lesson, we will create an app settings module that allows users to set font size, font family, theme, colors, and language. We will explore how to manage these settings using `GetX`.

### Setting Up the Project

Add the `get` dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  get: ^4.6.5
```

### App Settings Controller

First, let's create a controller to manage the app settings using `GetX`.

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

// Controller to manage app settings
class AppSettingsController extends GetxController {
  // Observable variable to track dark mode setting
  var isDarkMode = false.obs;

  // Method to toggle dark mode
  void toggleTheme() {
    isDarkMode.value = !isDarkMode.value;
  }

  // Observable variable to track font size
  var fontSize = 16.0.obs;

  // Method to set font size
  void setFontSize(double size) {
    fontSize.value = size;
  }

  // Observable variable to track font family
  var fontFamily = 'Roboto'.obs;

  // Method to set font family
  void setFontFamily(String family) {
    fontFamily.value = family;
  }

  // Observable variable to track primary color
  var primaryColor = Colors.blue.obs;

  // Method to set primary color
  void setPrimaryColor(Color color) {
    primaryColor.value = color;
  }

  // Observable variable to track locale (language setting)
  var locale = Locale('en').obs;

  // Method to set locale
  void setLocale(String languageCode) {
    locale.value = Locale(languageCode);
  }
}
```

### Integrating GetX

Next, integrate the `AppSettingsController` with `GetX`.

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

void main() {
  runApp(MyApp());
}

// Main application widget
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      // Initialize the AppSettingsController when the app starts
      initialBinding: BindingsBuilder(() {
        Get.put(AppSettingsController());
      }),
      // Set the app theme to light or dark based on the system settings
      theme: ThemeData.light(),
      darkTheme: ThemeData.dark(),
      themeMode: ThemeMode.system,
      // Set the app locale to the device's locale
      locale: Get.deviceLocale,
      home: HomeScreen(),
    );
  }
}
```

### Creating the Settings Screen

Create a settings screen where users can adjust the app settings.

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'app_settings_controller.dart';

// Settings screen where users can adjust app settings
class SettingsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Get the instance of AppSettingsController
    final AppSettingsController appSettings = Get.find<AppSettingsController>();

    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: ListView(
          children: [
            // Toggle for dark mode
            Obx(() => ListTile(
              title: Text('Dark Mode'),
              trailing: Switch(
                value: appSettings.isDarkMode.value,
                onChanged: (value) {
                  appSettings.toggleTheme();
                },
              ),
            )),
            // Slider for font size
            Obx(() => ListTile(
              title: Text('Font Size'),
              subtitle: Slider(
                min: 10,
                max: 30,
                value: appSettings.fontSize.value,
                onChanged: (value) {
                  appSettings.setFontSize(value);
                },
              ),
            )),
            // Dropdown for font family
            Obx(() => ListTile(
              title: Text('Font Family'),
              subtitle: DropdownButton<String>(
                value: appSettings.fontFamily.value,
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
            )),
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
            Obx(() => ListTile(
              title: Text('Language'),
              subtitle: DropdownButton<Locale>(
                value: appSettings.locale.value,
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
            )),
          ],
        ),
      ),
    );
  }
}
```

### Applying Settings to the App

Modify the main app to apply the settings from `AppSettingsController`.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Get the instance of AppSettingsController
    final AppSettingsController appSettings = Get.find<AppSettingsController>();

    return Obx(() => GetMaterialApp(
      // Apply theme settings
      theme: ThemeData(
        brightness: appSettings.isDarkMode.value ? Brightness.dark : Brightness.light,
        primaryColor: appSettings.primaryColor.value,
        textTheme: TextTheme(
          bodyText2: TextStyle(
            fontSize: appSettings.fontSize.value,
            fontFamily: appSettings.fontFamily.value,
          ),
        ),
      ),
      // Apply locale settings
      locale: appSettings.locale.value,
      home: HomeScreen(),
    ));
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
          Get.to(SettingsScreen());
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
import 'package:get/get.dart';

void main() {
  runApp(MyApp());
}

// Controller to manage app settings
class AppSettingsController extends GetxController {
  // Observable variable to track dark mode setting
  var isDarkMode = false.obs;

  // Method to toggle dark mode
  void toggleTheme() {
    isDarkMode.value = !isDarkMode.value;
  }

  // Observable variable to track font size
  var fontSize = 16.0.obs;

  // Method to set font size
  void setFontSize(double size) {
    fontSize.value = size;
  }

  // Observable variable to track font family
  var fontFamily = 'Roboto'.obs;

  // Method to set font family
  void setFontFamily(String family) {
    fontFamily.value = family;
  }

  // Observable variable to track primary color
  var primaryColor = Colors.blue.obs;

  // Method to set primary color
  void setPrimaryColor(Color color) {
    primaryColor.value = color;
  }

  // Observable variable to track locale (language setting)
  var locale = Locale('en').obs;

  // Method to set locale
  void setLocale(String languageCode) {
    locale.value = Locale(languageCode);
  }
}

// Main application widget
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Initialize the AppSettingsController when the app starts
    final AppSettingsController appSettings = Get.put(AppSettingsController());

    return Obx(() => GetMaterialApp(
      // Apply theme settings
      theme: ThemeData(
        brightness: appSettings.isDarkMode.value ? Brightness.dark : Brightness.light,
        primaryColor: appSettings.primaryColor.value,
        textTheme: TextTheme(
          bodyText2: TextStyle(
            fontSize: appSettings.fontSize.value,
            fontFamily: appSettings.fontFamily.value,
          ),
        ),
      ),
      // Apply locale settings
      locale: appSettings.locale.value,
      home: HomeScreen(),
    ));
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
          Get.to(SettingsScreen());
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
    // Get the instance of AppSettingsController
    final AppSettingsController appSettings = Get.find<AppSettingsController>();

    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: ListView(
          children: [
            // Toggle for dark mode
            Obx(() => ListTile(
              title: Text('Dark Mode'),
              trailing: Switch(
                value: appSettings.isDarkMode.value,
                onChanged: (value) {
                  appSettings.toggleTheme();
                },
              ),
            )),
            // Slider for font size
            Obx(() => ListTile(
              title: Text('Font Size'),
              subtitle: Slider(
                min: 10,
                max: 30,
                value: appSettings.fontSize.value,
                onChanged: (value) {
                  appSettings.setFontSize(value);
                },
              ),
            )),
            // Dropdown for font family
            Obx(() => ListTile(
              title: Text('Font Family'),
              subtitle: DropdownButton<String>(
                value: appSettings.fontFamily.value,
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
            )),
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
            Obx(() => ListTile(
              title: Text('Language'),
              subtitle: DropdownButton<Locale>(
                value: appSettings.locale.value,
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
            )),
          ],
        ),
      ),
    );
  }
}
```
