# Lesson 2: Using MaterialApp

Overview: How to use MaterialApp in a Flutter project.

## Key Concepts

- Creating a MaterialApp 🏗️
- Defining Routes 🛤️
- Theming Your App 🎨

## Creating a `MaterialApp` 🏗️

The `MaterialApp` widget is the starting point of a Material Design app.

  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        title: 'Material App Demo',
        home: HomeScreen(),
      );
    }
  }

  class HomeScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Home Screen'),
        ),
        body: Center(
          child: Text('Welcome to the Home Screen!'),
        ),
      );
    }
  }
  ```

## Defining Routes 🛤️

Routes are defined in the MaterialApp widget to navigate between screens.

```dart

MaterialApp(
  routes: {
    '/': (context) => HomeScreen(),
    '/second': (context) => SecondScreen(),
  },
);
```

## Theming Your App 🎨

The MaterialApp widget allows you to define a theme for your app.

```dart

MaterialApp(
  theme: ThemeData(
    primarySwatch: Colors.blue,
    textTheme: TextTheme(
      bodyText2: TextStyle(color: Colors.red),
    ),
  ),
);
```
