Lesson 1: TextField
Overview: Using TextField for user input and customizing its appearance.

Key Concepts:

Basic Usage of TextField 📝
Customizing TextField Appearance 🎨
Basic Usage of TextField 📝

Creating a simple TextField:
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
          title: Text('TextField Example'),
        ),
        body: Padding(
          padding: const EdgeInsets.all(16.0),
          child: TextField(
            decoration: InputDecoration(
              labelText: 'Enter your name',
            ),
          ),
        ),
      ),
    );
  }
}
Customizing TextField Appearance 🎨

Styling the TextField with custom properties:
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
          title: Text('Styled TextField Example'),
        ),
        body: Padding(
          padding: const EdgeInsets.all(16.0),
          child: TextField(
            decoration: InputDecoration(
              labelText: 'Enter your email',
              hintText: 'example@example.com',
              prefixIcon: Icon(Icons.email),
              border: OutlineInputBorder(),
            ),
          ),
        ),
      ),
    );
  }
}