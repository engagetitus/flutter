Lesson 2: Stack and Positioned
Overview: Using Stack for overlapping widgets and Positioned for positioning.

Key Concepts:

Overlapping Widgets with Stack 🎨
Precise Positioning with Positioned 📍
Overlapping Widgets with Stack 🎨

Creating overlapping layouts with Stack:
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
          title: Text('Stack Layout Example'),
        ),
        body: Stack(
          children: <Widget>[
            // Base layer
            Container(
              color: Colors.red,
              height: 300,
              width: 300,
            ),
            // Middle layer
            Container(
              color: Colors.green,
              height: 200,
              width: 200,
            ),
            // Top layer
            Container(
              color: Colors.blue,
              height: 100,
              width: 100,
            ),
          ],
        ),
      ),
    );
  }
}
Precise Positioning with Positioned 📍

Using Positioned for precise positioning in a Stack:
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
          title: Text('Positioned Layout Example'),
        ),
        body: Stack(
          children: <Widget>[
            // Positioned widget for precise positioning
            Positioned(
              left: 50,
              top: 50,
              child: Container(
                color: Colors.red,
                height: 100,
                width: 100,
              ),
            ),
            Positioned(
              right: 50,
              bottom: 50,
              child: Container(
                color: Colors.green,
                height: 100,
                width: 100,
              ),
            ),
            Positioned(
              left: 100,
              top: 100,
              child: Container(
                color: Colors.blue,
                height: 100,
                width: 100,
              ),
            ),
          ],
        ),
      ),
    );
  }
}