Lesson 4: Hands-on Flutter Architecture
Overview: Practical session to explore Flutter architecture through a sample app.
Key Concepts:
Setting Up a New Flutter Project 🛠️
Exploring the Default Flutter Project Structure 🗂️
Modifying the Main App Widget 🔄

# Setting Up a New Flutter Project 🛠️
1. **Create a new Flutter project**:
  ```bash
  flutter create my_app
  cd my_app

Exploring the Default Flutter Project Structure 🗂️
lib/main.dart: The entry point for the application.
pubspec.yaml: The configuration file for your app, including dependencies.
Modifying the Main App Widget 🔄
Open lib/main.dart and modify the code:
dart

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
          title: Text('Flutter Architecture Demo'),  // App bar title
        ),
        body: Center(
          child: Text('Hello, Flutter Architecture!'),  // Centered text
        ),
      ),
    );
  }
}
Run the app:
bash

flutter run