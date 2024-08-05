
### Module 7: Interaction with Snackbars

#### Lesson 1: Introduction to Snackbars
- **Overview**: Basics of using snackbars for user feedback in Flutter.
- **Key Concepts**:
  - Showing a Snackbar 📣
  - Customizing Snackbar Appearance 🎨


# Showing a Snackbar 📣
- **Using the `ScaffoldMessenger` to show a snackbar**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: SnackbarScreen(),
      );
    }
  }

  class SnackbarScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Snackbar Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              ScaffoldMessenger.of(context).showSnackBar(
                SnackBar(
                  content: Text('This is a snackbar'),
                ),
              );
            },
            child: Text('Show Snackbar'),
          ),
        ),
      );
    }
  }```
  Customizing Snackbar Appearance 🎨
Applying custom styles to the snackbar:
``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CustomSnackbarScreen(),
    );
  }
}

class CustomSnackbarScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Snackbar Example'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            ScaffoldMessenger.of(context).showSnackBar(
              SnackBar(
                content: Text(
                  'This is a custom snackbar',
                  style: TextStyle(color: Colors.white),
                ),
                backgroundColor: Colors.purple,
                action: SnackBarAction(
                  label: 'Undo',
                  onPressed: () {
                    // Handle undo action
                  },
                  textColor: Colors.yellow,
                ),
              ),
            );
          },
          child: Text('Show Custom Snackbar'),
        ),
      ),
    );
  }
}
```