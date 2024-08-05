Lesson 1: Introduction to User Input
Overview: Basics of handling user input in Flutter.
Key Concepts:
Using TextField for User Input 📝
Customizing TextField Appearance 🎨

# Using `TextField` for User Input 📝
- **Basic usage of `TextField`**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: TextFieldScreen(),
      );
    }
  }

  class TextFieldScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('TextField Example'),
        ),
        body: Padding(
          padding: const EdgeInsets.all(16.0),
          child: TextField(
            decoration: InputDecoration(
              border: OutlineInputBorder(),
              labelText: 'Enter your name', // Label text for the TextField
            ),
          ),
        ),
      );
    }
  }
```
Customizing TextField Appearance 🎨
Applying custom styles to TextField:
dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CustomTextFieldScreen(),
    );
  }
}

class CustomTextFieldScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom TextField Example'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: TextField(
          decoration: InputDecoration(
            border: OutlineInputBorder(),
            labelText: 'Enter your email',
            hintText: 'example@example.com', // Placeholder text
            prefixIcon: Icon(Icons.email), // Icon at the beginning of the TextField
          ),
        ),
      ),
    );
  }
}
```
