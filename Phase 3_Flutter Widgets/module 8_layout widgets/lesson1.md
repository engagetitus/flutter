Lesson 1: Row and Column
Overview: Understanding the layout widgets Row and Column.

Key Concepts:

Creating Horizontal and Vertical Layouts 🏗️
MainAxisAlignment and CrossAxisAlignment 📏
Creating Horizontal and Vertical Layouts 🏗️

Using Row and Column to create layouts:
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
          title: Text('Row and Column Layout'),
        ),
        body: Column(
          children: <Widget>[
            // Row for horizontal layout
            Row(
              children: <Widget>[
                // Expanded widgets to divide space equally
                Expanded(
                  child: Container(
                    color: Colors.red,
                    height: 100,
                  ),
                ),
                Expanded(
                  child: Container(
                    color: Colors.green,
                    height: 100,
                  ),
                ),
                Expanded(
                  child: Container(
                    color: Colors.blue,
                    height: 100,
                  ),
                ),
              ],
            ),
            // Expanded widget to take remaining space
            Expanded(
              child: Container(
                color: Colors.yellow,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
MainAxisAlignment and CrossAxisAlignment 📏

Aligning children within Row and Column:
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
          title: Text('MainAxisAlignment and CrossAxisAlignment'),
        ),
        body: Column(
          mainAxisAlignment: MainAxisAlignment.center, // Center vertically
          crossAxisAlignment: CrossAxisAlignment.start, // Align to the start horizontally
          children: <Widget>[
            Container(
              color: Colors.red,
              height: 100,
              width: 100,
            ),
            Container(
              color: Colors.green,
              height: 100,
              width: 100,
            ),
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