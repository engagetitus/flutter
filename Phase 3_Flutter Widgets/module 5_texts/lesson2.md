
#### Lesson 2: Advanced Text Widgets
- **Overview**: Exploring advanced text widgets and their functionalities.
- **Key Concepts**:
  - RichText Widget 💬
  - TextSpan and TextStyle 🎨


# RichText Widget 💬
- **Using the `RichText` widget**:
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
            title: Text('RichText Widget Example'),
          ),
          body: Center(
            child: RichText(
              text: TextSpan(
                text: 'Hello, ',
                style: TextStyle(fontSize: 24, color: Colors.black),
                children: <TextSpan>[
                  TextSpan(
                    text: 'Flutter!',
                    style: TextStyle(fontWeight: FontWeight.bold, color: Colors.blue),
                  ),
                ],
              ),
            ),
          ),
        ),
      );
    }
  }
```
TextSpan and TextStyle 🎨
Combining TextSpan and TextStyle:
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
          title: Text('TextSpan and TextStyle Example'),
        ),
        body: Center(
          child: RichText(
            text: TextSpan(
              text: 'Welcome to ',
              style: TextStyle(fontSize: 24, color: Colors.black),
              children: <TextSpan>[
                TextSpan(
                  text: 'Flutter',
                  style: TextStyle(fontWeight: FontWeight.bold, color: Colors.blue),
                ),
                TextSpan(
                  text: ' development!',
                  style: TextStyle(fontStyle: FontStyle.italic, color: Colors.green),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```
