# Module 5: State Management with BLoC

## Lesson 2: Practical State Management - App Settings

In this lesson, we will create an app settings module that allows users to set font size, font family, theme, colors, and language. We will explore how to manage these settings using `BLoC` (Business Logic Component).

### Setting Up the Project

Add the `flutter_bloc` and `equatable` dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_bloc: ^7.0.0
  equatable: ^2.0.0
```

### App Settings Model and BLoC Setup

First, let's create the app settings model, events, state, and BLoC.

#### Events

```dart
import 'package:equatable/equatable.dart';
import 'package:flutter/material.dart';

abstract class AppSettingsEvent extends Equatable {
  const AppSettingsEvent();

  @override
  List<Object> get props => [];
}

class ToggleThemeEvent extends AppSettingsEvent {}

class SetFontSizeEvent extends AppSettingsEvent {
  final double fontSize;

  SetFontSizeEvent(this.fontSize);

  @override
  List<Object> get props => [fontSize];
}

class SetFontFamilyEvent extends AppSettingsEvent {
  final String fontFamily;

  SetFontFamilyEvent(this.fontFamily);

  @override
  List<Object> get props => [fontFamily];
}

class SetPrimaryColorEvent extends AppSettingsEvent {
  final Color color;

  SetPrimaryColorEvent(this.color);

  @override
  List<Object> get props => [color];
}

class SetLocaleEvent extends AppSettingsEvent {
  final String languageCode;

  SetLocaleEvent(this.languageCode);

  @override
  List<Object> get props => [languageCode];
}
```

#### State

```dart
import 'package:equatable/equatable.dart';
import 'package:flutter/material.dart';

class AppSettingsState extends Equatable {
  final bool isDarkMode;
  final double fontSize;
  final String fontFamily;
  final Color primaryColor;
  final Locale locale;

  const AppSettingsState({
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

  @override
  List<Object> get props => [isDarkMode, fontSize, fontFamily, primaryColor, locale];
}
```

#### BLoC

```dart
import 'package:bloc/bloc.dart';
import 'package:flutter/material.dart';
import 'app_settings_event.dart';
import 'app_settings_state.dart';

class AppSettingsBloc extends Bloc<AppSettingsEvent, AppSettingsState> {
  AppSettingsBloc()
      : super(AppSettingsState(
          isDarkMode: false,
          fontSize: 16.0,
          fontFamily: 'Roboto',
          primaryColor: Colors.blue,
          locale: Locale('en'),
        )) {
    on<ToggleThemeEvent>((event, emit) {
      emit(state.copyWith(isDarkMode: !state.isDarkMode));
    });

    on<SetFontSizeEvent>((event, emit) {
      emit(state.copyWith(fontSize: event.fontSize));
    });

    on<SetFontFamilyEvent>((event, emit) {
      emit(state.copyWith(fontFamily: event.fontFamily));
    });

    on<SetPrimaryColorEvent>((event, emit) {
      emit(state.copyWith(primaryColor: event.color));
    });

    on<SetLocaleEvent>((event, emit) {
      emit(state.copyWith(locale: Locale(event.languageCode)));
    });
  }
}
```

### Integrating BLoC

Next, integrate the `AppSettingsBloc` with the Flutter app.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';
import 'app_settings_bloc.dart';
import 'app_settings_event.dart';
import 'app_settings_state.dart';

void main() {
  runApp(MyApp());
}

// Main application widget
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocProvider(
      create: (context) => AppSettingsBloc(),
      child: BlocBuilder<AppSettingsBloc, AppSettingsState>(
        builder: (context, state) {
          return MaterialApp(
            theme: state.isDarkMode ? ThemeData.dark() : ThemeData.light(),
            locale: state.locale,
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
import 'package:flutter_bloc/flutter_bloc.dart';
import 'app_settings_bloc.dart';
import 'app_settings_event.dart';
import 'app_settings_state.dart';

// Settings screen where users can adjust app settings
class SettingsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: BlocBuilder<AppSettingsBloc, AppSettingsState>(
          builder: (context, state) {
            return ListView(
              children: [
                // Toggle for dark mode
                ListTile(
                  title: Text('Dark Mode'),
                  trailing: Switch(
                    value: state.isDarkMode,
                    onChanged: (value) {
                      context.read<AppSettingsBloc>().add(ToggleThemeEvent());
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
                      context.read<AppSettingsBloc>().add(SetFontSizeEvent(value));
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
                      context.read<AppSettingsBloc>().add(SetFontFamilyEvent(value!));
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
                          context.read<AppSettingsBloc>().add(SetPrimaryColorEvent(color));
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
                      context.read<AppSettingsBloc>().add(SetLocaleEvent(value!.languageCode));
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
  @override
  Widget build(BuildContext context) {
    return BlocProvider(
      create: (context) => AppSettingsBloc(),
      child: BlocBuilder<AppSettingsBloc, AppSettingsState>(
        builder: (context, state) {
          return MaterialApp(
            theme: ThemeData(
              brightness: state.isDarkMode ? Brightness.dark : Brightness.light,
              primaryColor: state.primaryColor,
              textTheme: TextTheme(
                bodyText2: TextStyle(
                  fontSize: state.fontSize,
                  fontFamily: state.fontFamily,
                ),
              ),
            ),
            locale: state.locale,
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
```

### Complete Code

Here’s the complete code for the app with comments:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';
import 'package:equatable/equatable.dart';

void main() {
  runApp(MyApp());
}

// Events
abstract class AppSettingsEvent extends Equatable {
  const AppSettingsEvent();

  @override
  List<Object> get props => [];
}

class Toggle

ThemeEvent extends AppSettingsEvent {}

class SetFontSizeEvent extends AppSettingsEvent {
  final double fontSize;

  SetFontSizeEvent(this.fontSize);

  @override
  List<Object> get props => [fontSize];
}

class SetFontFamilyEvent extends AppSettingsEvent {
  final String fontFamily;

  SetFontFamilyEvent(this.fontFamily);

  @override
  List<Object> get props => [fontFamily];
}

class SetPrimaryColorEvent extends AppSettingsEvent {
  final Color color;

  SetPrimaryColorEvent(this.color);

  @override
  List<Object> get props => [color];
}

class SetLocaleEvent extends AppSettingsEvent {
  final String languageCode;

  SetLocaleEvent(this.languageCode);

  @override
  List<Object> get props => [languageCode];
}

// State
class AppSettingsState extends Equatable {
  final bool isDarkMode;
  final double fontSize;
  final String fontFamily;
  final Color primaryColor;
  final Locale locale;

  const AppSettingsState({
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

  @override
  List<Object> get props => [isDarkMode, fontSize, fontFamily, primaryColor, locale];
}

// BLoC
class AppSettingsBloc extends Bloc<AppSettingsEvent, AppSettingsState> {
  AppSettingsBloc()
      : super(AppSettingsState(
          isDarkMode: false,
          fontSize: 16.0,
          fontFamily: 'Roboto',
          primaryColor: Colors.blue,
          locale: Locale('en'),
        )) {
    on<ToggleThemeEvent>((event, emit) {
      emit(state.copyWith(isDarkMode: !state.isDarkMode));
    });

    on<SetFontSizeEvent>((event, emit) {
      emit(state.copyWith(fontSize: event.fontSize));
    });

    on<SetFontFamilyEvent>((event, emit) {
      emit(state.copyWith(fontFamily: event.fontFamily));
    });

    on<SetPrimaryColorEvent>((event, emit) {
      emit(state.copyWith(primaryColor: event.color));
    });

    on<SetLocaleEvent>((event, emit) {
      emit(state.copyWith(locale: Locale(event.languageCode)));
    });
  }
}

// Main application widget
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocProvider(
      create: (context) => AppSettingsBloc(),
      child: BlocBuilder<AppSettingsBloc, AppSettingsState>(
        builder: (context, state) {
          return MaterialApp(
            // Apply theme settings
            theme: ThemeData(
              brightness: state.isDarkMode ? Brightness.dark : Brightness.light,
              primaryColor: state.primaryColor,
              textTheme: TextTheme(
                bodyText2: TextStyle(
                  fontSize: state.fontSize,
                  fontFamily: state.fontFamily,
                ),
              ),
            ),
            // Apply locale settings
            locale: state.locale,
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
        child: BlocBuilder<AppSettingsBloc, AppSettingsState>(
          builder: (context, state) {
            return ListView(
              children: [
                // Toggle for dark mode
                ListTile(
                  title: Text('Dark Mode'),
                  trailing: Switch(
                    value: state.isDarkMode,
                    onChanged: (value) {
                      context.read<AppSettingsBloc>().add(ToggleThemeEvent());
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
                      context.read<AppSettingsBloc>().add(SetFontSizeEvent(value));
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
                      context.read<AppSettingsBloc>().add(SetFontFamilyEvent(value!));
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
                          context.read<AppSettingsBloc>().add(SetPrimaryColorEvent(color));
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
                      context.read<AppSettingsBloc>().add(SetLocaleEvent(value!.languageCode));
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
