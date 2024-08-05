
#### Lesson 4: Practical Examples with Text Widgets
- **Overview**: Hands-on examples to demonstrate the use of various text widget properties.
- **Key Concepts**:
  - Creating a Styled Text Widget 🎨
  - Combining RichText and TextSpan 💬


# Creating a Styled Text Widget 🎨
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
        title: 'Styled Text Demo',
        home: StyledTextScreen(),
      );
    }
  }

  class StyledTextScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Styled Text Example'),
        ),
        body: Center(
          child: Text(
            'Hello, Flutter!',
            style: TextStyle(
              fontSize: 24,
              fontWeight: FontWeight.bold,
              color: Colors.blue,
              letterSpacing: 2.0,
              wordSpacing: 5.0,
              decoration: TextDecoration.underline,
              decorationStyle: TextDecorationStyle.dashed,
            ),
          ),
        ),
      );
    }
  }
Combining RichText and TextSpan 💬
Creating a complex text layout:
``` dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'RichText and TextSpan Demo',
      home: RichTextScreen(),
    );
  }
}

class RichTextScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('RichText Example'),
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
              TextSpan(
                text: ' How are you today?',
                style: TextStyle(fontStyle: FontStyle.italic, color: Colors.green),
              ),
            ],
          ),
        ),
      ),
    );
  }
}