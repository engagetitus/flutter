
### Module 3: Pub.dev

#### Lesson 1: Introduction to Pub.dev
- **Overview**: Basics of using `pub.dev` for managing Flutter packages.
- **Key Concepts**:
  - What is `pub.dev`? 🌐
  - Adding Packages to Your Project 📦


# What is `pub.dev`? 🌐
`pub.dev` is the package manager for the Dart programming language and Flutter framework. It hosts a wide range of packages that developers can use to add functionality to their applications.

# Adding Packages to Your Project 📦
- **Adding a package to your Flutter project**:
  ```dart
  import 'package:flutter/material.dart';
  import 'package:http/http.dart' as http; // Example of importing a package

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: PubDevExampleScreen(),
      );
    }
  }

  class PubDevExampleScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('pub.dev Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              // Example usage of the http package
              http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'))
                  .then((response) {
                print(response.body);
              });
            },
            child: Text('Fetch Data'),
          ),
        ),
      );
    }
  }
```
Updating pubspec.yaml:
yaml

name: my_app
description: A new Flutter project.

dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.3 # Adding the http package
  ```
  