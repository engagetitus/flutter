
### Module 4: Refactor with Flutter Custom Widgets

#### Lesson 1: Introduction to Custom Widgets
- **Overview**: Basics of creating custom widgets in Flutter.
- **Key Concepts**:
  - Stateless vs Stateful Widgets 🧩
  - Creating a Stateless Widget 📜


# Stateless vs Stateful Widgets 🧩
- **Understanding the difference between stateless and stateful widgets**:
  - **Stateless Widgets**: Immutable, meaning their properties can't change once they're created.
  - **Stateful Widgets**: Mutable, meaning they can change over time and hold state.

# Creating a Stateless Widget 📜
- **Building a custom stateless widget**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: CustomStatelessWidgetScreen(),
      );
    }
  }

  class CustomStatelessWidgetScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Custom Stateless Widget'),
        ),
        body: Center(
          child: CustomStatelessWidget(
            text: 'Hello, Flutter!',
          ),
        ),
      );
    }
  }

  class CustomStatelessWidget extends StatelessWidget {
    final String text;

    CustomStatelessWidget({required this.text});

    @override
    Widget build(BuildContext context) {
      return Text(
        text,
        style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
      );
    }
  }
```
