Lesson 3: GridView
Overview: Creating grids with GridView and customizing layouts.

Key Concepts:

Creating Simple Grids 📐
Customizing Grid Layouts 🎨
Creating Simple Grids 📐

Using GridView to create a simple grid layout:
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
          title: Text('Simple Grid Example'),
        ),
        body: GridView.count(
          crossAxisCount: 2, // Number of columns
          children: List.generate(6, (index) {
            return Container(
              color: Colors.blue[(index + 1) * 100],
              child: Center(
                child: Text(
                  'Item $index',
                  style: TextStyle(color: Colors.white),
                ),
              ),
            );
          }),
        ),
      ),
    );
  }
}
Customizing Grid Layouts 🎨

Customizing the layout of a GridView:
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
          title: Text('Custom Grid Example'),
        ),
        body: GridView.builder(
          gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
            crossAxisCount: 3, // Number of columns
            crossAxisSpacing: 10, // Spacing between columns
            mainAxisSpacing: 10, // Spacing between rows
          ),
          itemBuilder: (context, index) {
            return Container(
              color: Colors.blue[(index % 9 + 1) * 100],
              child: Center(
                child: Text(
                  'Item $index',
                  style: TextStyle(color: Colors.white),
                ),
              ),
            );
          },
          itemCount: 30, // Number of items
        ),
      ),
    );
  }
}