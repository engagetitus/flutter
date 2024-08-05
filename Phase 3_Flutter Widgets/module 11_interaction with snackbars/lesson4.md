
#### Lesson 4: Practical Examples with Snackbars
- **Overview**: Hands-on examples to demonstrate the use of various snackbar properties.
- **Key Concepts**:
  - Custom Snackbar Designs 🎨
  - Multi-action Snackbars 🛠️


# Custom Snackbar Designs 🎨
- **Open `lib/main.dart` and modify the code**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        title: 'Custom Snackbar Demo',
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
Multi-action Snackbars 🛠️
Adding multiple actions to a snackbar:
``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Multi-action Snackbar Demo',
      home: MultiActionSnackbarScreen(),
    );
  }
}

class MultiActionSnackbarScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Multi-action Snackbar Example'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            ScaffoldMessenger.of(context).showSnackBar(
              SnackBar(
                content: Text('This snackbar has multiple actions'),
                action: SnackBarAction(
                  label: 'Undo',
                  onPressed: () {
                    ScaffoldMessenger.of(context).showSnackBar(
                      SnackBar(
                        content: Text('Undo action'),
                      ),
                    );
                  },
                ),
                duration: Duration(seconds: 5),
                onVisible: () {
                  ScaffoldMessenger.of(context).showSnackBar(
                    SnackBar(
                      content: Text('Another action can be added here'),
                    ),
                  );
                },
              ),
            );
          },
          child: Text('Show Multi-action Snackbar'),
        ),
      ),
    );
  }
}