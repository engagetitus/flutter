
# Lesson 1: Introduction to Shared Preferences

**Objective:** Understand the basics of Shared Preferences in Flutter.

**Topics Covered:**

- What is Shared Preferences?
- When to use Shared Preferences.
- Installation and setup.

## What is Shared Preferences?

Shared Preferences is a simple key-value store provided by Flutter to store small amounts of data persistently. It allows you to save and retrieve simple data types (such as strings, integers, booleans, doubles, and lists of strings) that need to be retained across app sessions.

### When to Use Shared Preferences

- **Storing User Settings:** For example, theme preferences, language settings, or notification preferences.
- **Caching Small Amounts of Data:** For example, user tokens, app state, or temporary data.
- **Saving Simple State Information:** For example, remembering the last visited page or user input.

## Installation and Setup

### Step 1: Add the Dependency

Add the `shared_preferences` package to your `pubspec.yaml` file:

```yaml
dependencies:
  shared_preferences: ^2.0.6
```

Run `flutter pub get` to install the package.

### Step 2: Import the Package

Import the `shared_preferences` package in your Dart file:

```dart
import 'package:shared_preferences/shared_preferences.dart';
```

### Step 3: Initialize Shared Preferences

Before using Shared Preferences, you need to initialize an instance of the `SharedPreferences` class. This is typically done in the `main` function of your app.

```dart
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  SharedPreferences prefs = await SharedPreferences.getInstance();
  runApp(MyApp(prefs: prefs));
}

class MyApp extends StatelessWidget {
  final SharedPreferences prefs;

  MyApp({required this.prefs});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HomePage(prefs: prefs),
    );
  }
}

class HomePage extends StatelessWidget {
  final SharedPreferences prefs;

  HomePage({required this.prefs});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Shared Preferences Example'),
      ),
      body: Center(
        child: Text('Welcome to Shared Preferences Example'),
      ),
    );
  }
}
```

### Summary

In this lesson, you learned:

- What Shared Preferences is and its use cases.
- How to add the `shared_preferences` package to your Flutter project.
- How to initialize Shared Preferences in your app.

Shared Preferences is a powerful tool for persisting simple data in your Flutter applications. In the next lessons, we will explore how to save, retrieve, and manage data using Shared Preferences.
