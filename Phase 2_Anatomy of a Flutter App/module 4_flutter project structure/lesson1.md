
# Module 4: Flutter Project Structure

## Lesson 1: Understanding Flutter Project Structure

- **Overview**: Overview of the default Flutter project structure.
- **Key Concepts**:
  - Project Directories and Files 📂
  - `lib` Directory 📁
  - `pubspec.yaml` 📜

# Project Directories and Files 📂

- The default Flutter project includes several directories and files:
  - `android`: Android-specific files.
  - `ios`: iOS-specific files.
  - `lib`: The main directory for Dart code.
  - `test`: Directory for unit tests.
  - `pubspec.yaml`: Configuration file.

# `lib` Directory 📁

- The `lib` directory is where you write your Dart code. It contains:
  - `main.dart`: The entry point for the app.

  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: Scaffold(
          appBar: AppBar(
            title: Text('Flutter Project Structure'),
          ),
          body: Center(
            child: Text('Hello, Flutter!'),
          ),
        ),
      );
    }
  }
  ```

## pubspec.yaml 📜

The pubspec.yaml file is used to manage dependencies, assets, and other configuration options.

```yaml

name: my_app
description: A new Flutter project.

environment:
  sdk: ">=2.12.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter

dev_dependencies:
  flutter_test:
    sdk: flutter

flutter:
  uses-material-design: true

  assets:
    - images/
```
