
#### Lesson 3: Text Alignment and Overflow
- **Overview**: Managing text alignment and handling overflow in Flutter.
- **Key Concepts**:
  - Aligning Text 📝
  - Handling Text Overflow 🌊


# Aligning Text 📝
- **Aligning text within a container**:
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
            title: Text('Text Alignment Example'),
          ),
          body: Container(
            alignment: Alignment.center,
            child: Text(
              'Centered Text',
              textAlign: TextAlign.center,  // Aligning text
              style: TextStyle(fontSize: 24),
            ),
          ),
        ),
      );
    }
  }
Handling Text Overflow 🌊
Handling overflow using TextOverflow:
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
          title: Text('Text Overflow Example'),
        ),
        body: Center(
          child: Container(
            width: 200,
            child: Text(
              'This is a very long text that might overflow.',
              overflow: TextOverflow.ellipsis,  // Handling overflow
              style: TextStyle(fontSize: 24),
            ),
          ),
        ),
      ),
    );
  }
}  
