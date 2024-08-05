# Lesson 1: Basic Text Widgets

- **Overview**: Introduction to the basic text widgets in Flutter.
- **Key Concepts**:
  - Text Widget Basics 📄
  - Styling Text 🎨

## Text Widget Basics 📄

- **Using the `Text` widget**:

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
            title: Text('Text Widget Example'),
          ),
          body: Center(
            child: Text('Hello, Flutter!'),  // Basic Text widget
          ),
        ),
      );
    }
  }

  ```

## Styling Text 🎨

Applying styles to the Text widget:

``` dart

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
          title: Text('Styled Text Example'),
        ),
        body: Center(
          child: Text(
            'Hello, Flutter!',
            style: TextStyle(
              fontSize: 24,  // Font size
              fontWeight: FontWeight.bold,  // Bold text
              color: Colors.blue,  // Text color
            ),
          ),
        ),
      ),
    );
  }
}
```
