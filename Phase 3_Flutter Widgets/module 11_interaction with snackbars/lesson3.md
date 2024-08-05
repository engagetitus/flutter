
#### Lesson 3: Interaction with Snackbar Actions
- **Overview**: Handling user interactions with snackbar actions.
- **Key Concepts**:
  - Adding Actions to Snackbars 🛠️
  - Handling Snackbar Action Clicks 🖱️


# Adding Actions to Snackbars 🛠️
- **Adding an action button to the snackbar**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: SnackbarActionScreen(),
      );
    }
  }

  class SnackbarActionScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Snackbar Action Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              ScaffoldMessenger.of(context).showSnackBar(
                SnackBar(
                  content: Text('This snackbar has an action'),
                  action: SnackBarAction(
                    label: 'Undo',
                    onPressed: () {
                      // Handle undo action
                    },
                  ),
                ),
              );
            },
            child: Text('Show Snackbar with Action'),
          ),
        ),
      );
    }
  }
Handling Snackbar Action Clicks 🖱️
Handling the click event of the snackbar action:
``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: SnackbarClickActionScreen(),
    );
  }
}

class SnackbarClickActionScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Snackbar Click Action Example'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            ScaffoldMessenger.of(context).showSnackBar(
              SnackBar(
                content: Text('Click the action to undo'),
                action: SnackBarAction(
                  label: 'Undo',
                  onPressed: () {
                    ScaffoldMessenger.of(context).showSnackBar(
                      SnackBar(
                        content: Text('Action undone'),
                      ),
                    );
                  },
                ),
              ),
            );
          },
          child: Text('Show Snackbar with Click Action'),
        ),
      ),
    );
  }
}