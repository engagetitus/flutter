
#### Lesson 2: Advanced Snackbar Techniques
- **Overview**: Exploring advanced techniques for using snackbars in Flutter.
- **Key Concepts**:
  - Using Snackbars with ScaffoldMessenger 📤
  - Persistent Snackbars 📌


# Using Snackbars with ScaffoldMessenger 📤
- **Using `ScaffoldMessenger` for more control over snackbars**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: AdvancedSnackbarScreen(),
      );
    }
  }

  class AdvancedSnackbarScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Advanced Snackbar Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              final messenger = ScaffoldMessenger.of(context);
              final snackbar = SnackBar(
                content: Text('This is an advanced snackbar'),
              );
              messenger.showSnackBar(snackbar);
            },
            child: Text('Show Advanced Snackbar'),
          ),
        ),
      );
    }
  }
```
Persistent Snackbars 📌
Creating snackbars that stay until dismissed:
``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: PersistentSnackbarScreen(),
    );
  }
}

class PersistentSnackbarScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Persistent Snackbar Example'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            final messenger = ScaffoldMessenger.of(context);
            final snackbar = SnackBar(
              content: Text('This snackbar stays until dismissed'),
              duration: Duration(days: 365),
            );
            messenger.showSnackBar(snackbar);
          },
          child: Text('Show Persistent Snackbar'),
        ),
      ),
    );
  }
}
```
