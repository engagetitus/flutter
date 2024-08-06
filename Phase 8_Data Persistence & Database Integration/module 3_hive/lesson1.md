
# Lesson 1: Introduction to Hive

**Objective:** Understand the basics of Hive in Flutter.

**Topics Covered:**

- What is Hive?
- When to use Hive.
- Installation and setup.

## What is Hive?

Hive is a lightweight and blazing-fast key-value database written in Dart for Flutter applications.

### When to Use Hive

- Storing large amounts of unstructured data.
- When performance is a critical factor.
- Offline data storage.

## Installation and Setup

1. Add the dependency to `pubspec.yaml`:

    ```yaml
    dependencies:
      hive: ^2.0.0
      hive_flutter: ^1.1.0
    ```

2. Import the packages in your Dart file:

    ```dart
    import 'package:hive/hive.dart';
    import 'package:hive_flutter/hive_flutter.dart';
    ```

3. Initialize Hive:

    ```dart
    void main() async {
      await Hive.initFlutter();
      runApp(MyApp());
    }
    ```
