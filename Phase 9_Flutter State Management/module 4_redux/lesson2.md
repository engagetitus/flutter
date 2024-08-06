# Module 4: State Management with Redux

## Lesson 2: Practical State Management - App Settings

In this lesson, we will create an app settings module that allows users to set font size, font family, theme, colors, and language. We will explore how to manage these settings using `Redux`.

### Setting Up the Project

Add the `flutter_redux` and `redux` dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_redux: ^0.8.0
  redux: ^4.0.0
```

### App Settings Model and Redux Setup

First, let's create the app settings model, actions, reducer, and store.

#### Actions

```dart
class ToggleThemeAction {}

class SetFontSizeAction {
  final double fontSize;
  SetFontSizeAction(this.fontSize);
}

class SetFontFamilyAction {
  final String fontFamily;
  SetFontFamilyAction(this.fontFamily);
}

class SetPrimaryColorAction {
  final Color color;
  SetPrimaryColorAction(this.color);
}

class SetLocaleAction {
  final String languageCode;
  SetLocaleAction(this.languageCode);
}
```

#### App Settings State

```dart
import 'package:flutter/material.dart';

class AppSettingsState {
  final bool isDarkMode;
  final double fontSize;
  final String fontFamily;
  final Color primaryColor;
  final Locale locale;

  AppSettingsState({
    required this.isDarkMode,
    required this.fontSize,
    required this.fontFamily,
    required this.primaryColor,
    required this.locale,
  });

  AppSettingsState copyWith({
    bool? isDarkMode,
    double? fontSize,
    String? fontFamily,
    Color? primaryColor,
    Locale? locale,
  }) {
    return AppSettingsState(
      isDarkMode: isDarkMode ?? this.isDarkMode,
      fontSize: fontSize ?? this.fontSize,
      fontFamily: fontFamily ?? this.fontFamily,
      primaryColor: primaryColor ?? this.primaryColor,
      locale: locale ?? this.locale,
    );
  }
}
```

#### Reducer

```dart
AppSettingsState appSettingsReducer(AppSettingsState state, dynamic action) {
  if (action is ToggleThemeAction) {
    return state.copyWith(isDarkMode: !state.isDarkMode);
  } else if (action is SetFontSizeAction) {
    return state.copyWith(fontSize: action.fontSize);
  } else if (action is SetFontFamilyAction) {
    return state.copyWith(fontFamily: action.fontFamily);
  } else if (action is SetPrimaryColorAction) {
    return state.copyWith(primaryColor: action.color);
  } else if (action is SetLocaleAction) {
    return state.copyWith(locale: Locale(action.languageCode));
  }
  return state;
}
```

#### Store

```dart
import 'package:redux/redux.dart';

final store = Store<AppSettingsState>(
  appSettingsReducer,
  initialState: AppSettingsState(
    isDarkMode: false,
    fontSize: 16.0,
    fontFamily: 'Roboto',
    primaryColor: Colors.blue,
    locale: Locale('en'),
  ),
);
```

### Integrating Redux

Next, integrate the `AppSettingsState` with `Redux`.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_redux/flutter_redux.dart';
import 'package:redux/redux.dart';

void main() {
  runApp(MyApp(store: store));
}

// Main application widget
class MyApp extends StatelessWidget {
  final Store<AppSettingsState> store;

  MyApp({required this.store});

  @override
  Widget build(BuildContext context) {
    return StoreProvider(
      store: store,
      child: StoreBuilder<AppSettingsState>(
        builder: (context, store) {
          return MaterialApp(
            theme: store.state.isDarkMode ? ThemeData.dark() : ThemeData.light(),
            locale: store.state.locale,
            home: HomeScreen(),
          );
        },
      ),
    );
  }
}
```

### Creating the Settings Screen

Create a settings screen where users can adjust the app settings.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_redux/flutter_redux.dart';

class SettingsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: StoreConnector<AppSettingsState, AppSettingsState>(
          converter: (store) => store.state,
          builder: (context, state) {
            return ListView(
              children: [
                // Toggle for dark mode
                ListTile(
                  title: Text('Dark Mode'),
                  trailing: Switch(
                    value: state.isDarkMode,
                    onChanged: (value) {
                      StoreProvider.of<AppSettingsState>(context).dispatch(ToggleThemeAction());
                    },
                  ),
                ),
                // Slider for font size
                ListTile(
                  title: Text('Font Size'),
                  subtitle: Slider(
                    min: 10,
                    max: 30,
                    value: state.fontSize,
                    onChanged: (value) {
                      StoreProvider.of<AppSettingsState>(context).dispatch(SetFontSizeAction(value));
                    },
                  ),
                ),
                // Dropdown for font family
                ListTile(
                  title: Text('Font Family'),
                  subtitle: DropdownButton<String>(
                    value: state.fontFamily,
                    items: ['Roboto', 'Arial', 'Times New Roman'].map((String value) {
                      return DropdownMenuItem<String>(
                        value: value,
                        child: Text(value),
                      );
                    }).toList(),
                    onChanged: (value) {
                      StoreProvider.of<AppSettingsState>(context).dispatch(SetFontFamilyAction(value!));
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
                          StoreProvider.of<AppSettingsState>(context).dispatch(SetPrimaryColorAction(color));
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
                    value: state.locale,
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
                      StoreProvider.of<AppSettingsState>(context).dispatch(SetLocaleAction(value!.languageCode));
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

Modify the main app to apply the settings from `AppSettingsState`.

```dart
class MyApp extends StatelessWidget {
  final Store<AppSettingsState> store;

  MyApp({required this.store});

  @override
  Widget build(BuildContext context) {
    return StoreProvider(
      store: store,
      child: StoreBuilder<AppSettingsState>(
        builder: (context, store) {
          return MaterialApp(
            theme: ThemeData(
              brightness: store.state.isDarkMode ? Brightness.dark : Brightness.light,
              primaryColor: store.state.primaryColor,
              textTheme: TextTheme(
                bodyText2: TextStyle(
                  fontSize: store.state.fontSize,
                  fontFamily: store.state.fontFamily,
                ),
              ),
            ),
            locale: store.state.locale,
            home: HomeScreen(),
          );
        },
      ),
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
import 'package:flutter_redux/flutter_redux.dart';
import 'package:redux/redux.dart';

void main() {
  runApp(MyApp(store: store));
}

// Actions
class ToggleThemeAction {}

class SetFontSizeAction {
  final double fontSize;
  SetFontSizeAction(this.fontSize);
}

class SetFontFamilyAction {
  final String fontFamily;
  SetFontFamilyAction(this.fontFamily);
}

class SetPrimaryColorAction {
  final Color color;
  SetPrimaryColorAction(this.color);
}

class SetLocaleAction {
  final String languageCode;
  SetLocaleAction(this.languageCode);
}

// AppSettings State
class AppSettingsState {
  final bool isDarkMode;
  final double fontSize;
  final String fontFamily;
  final Color primaryColor;
  final Locale locale;

  AppSettingsState({
    required this.isDarkMode,
    required this.fontSize,
    required this.fontFamily,
    required this.primaryColor,
    required this.locale,
  });

  AppSettingsState copyWith({
    bool? isDarkMode,
    double? fontSize,
    String? fontFamily,
    Color? primaryColor,
    Locale? locale,
  }) {
    return AppSettingsState(
      isDarkMode: isDark

Mode ?? this.isDarkMode,
      fontSize: fontSize ?? this.fontSize,
      fontFamily: fontFamily ?? this.fontFamily,
      primaryColor: primaryColor ?? this.primaryColor,
      locale: locale ?? this.locale,
    );
  }
}

// Reducer
AppSettingsState appSettingsReducer(AppSettingsState state, dynamic action) {
  if (action is ToggleThemeAction) {
    return state.copyWith(isDarkMode: !state.isDarkMode);
  } else if (action is SetFontSizeAction) {
    return state.copyWith(fontSize: action.fontSize);
  } else if (action is SetFontFamilyAction) {
    return state.copyWith(fontFamily: action.fontFamily);
  } else if (action is SetPrimaryColorAction) {
    return state.copyWith(primaryColor: action.color);
  } else if (action is SetLocaleAction) {
    return state.copyWith(locale: Locale(action.languageCode));
  }
  return state;
}

// Store
final store = Store<AppSettingsState>(
  appSettingsReducer,
  initialState: AppSettingsState(
    isDarkMode: false,
    fontSize: 16.0,
    fontFamily: 'Roboto',
    primaryColor: Colors.blue,
    locale: Locale('en'),
  ),
);

// Main application widget
class MyApp extends StatelessWidget {
  final Store<AppSettingsState> store;

  MyApp({required this.store});

  @override
  Widget build(BuildContext context) {
    return StoreProvider(
      store: store,
      child: StoreBuilder<AppSettingsState>(
        builder: (context, store) {
          return MaterialApp(
            // Apply theme settings
            theme: ThemeData(
              brightness: store.state.isDarkMode ? Brightness.dark : Brightness.light,
              primaryColor: store.state.primaryColor,
              textTheme: TextTheme(
                bodyText2: TextStyle(
                  fontSize: store.state.fontSize,
                  fontFamily: store.state.fontFamily,
                ),
              ),
            ),
            // Apply locale settings
            locale: store.state.locale,
            home: HomeScreen(),
          );
        },
      ),
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
class SettingsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: StoreConnector<AppSettingsState, AppSettingsState>(
          converter: (store) => store.state,
          builder: (context, state) {
            return ListView(
              children: [
                // Toggle for dark mode
                ListTile(
                  title: Text('Dark Mode'),
                  trailing: Switch(
                    value: state.isDarkMode,
                    onChanged: (value) {
                      StoreProvider.of<AppSettingsState>(context).dispatch(ToggleThemeAction());
                    },
                  ),
                ),
                // Slider for font size
                ListTile(
                  title: Text('Font Size'),
                  subtitle: Slider(
                    min: 10,
                    max: 30,
                    value: state.fontSize,
                    onChanged: (value) {
                      StoreProvider.of<AppSettingsState>(context).dispatch(SetFontSizeAction(value));
                    },
                  ),
                ),
                // Dropdown for font family
                ListTile(
                  title: Text('Font Family'),
                  subtitle: DropdownButton<String>(
                    value: state.fontFamily,
                    items: ['Roboto', 'Arial', 'Times New Roman'].map((String value) {
                      return DropdownMenuItem<String>(
                        value: value,
                        child: Text(value),
                      );
                    }).toList(),
                    onChanged: (value) {
                      StoreProvider.of<AppSettingsState>(context).dispatch(SetFontFamilyAction(value!));
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
                          StoreProvider.of<AppSettingsState>(context).dispatch(SetPrimaryColorAction(color));
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
                    value: state.locale,
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
                      StoreProvider.of<AppSettingsState>(context).dispatch(SetLocaleAction(value!.languageCode));
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
