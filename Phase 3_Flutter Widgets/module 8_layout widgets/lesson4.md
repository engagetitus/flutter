Lesson 4: ListView
Overview: Building scrollable lists with ListView and optimizing performance.

Key Concepts:

Creating Simple Lists 📜
Optimizing List Performance 🚀
Creating Simple Lists 📜

Using ListView to create a simple list:
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
          title: Text('Simple List Example'),
        ),
        body: ListView(
          children: List.generate(10, (index) {
            return ListTile(
              title: Text('Item $index'),
            );
          }),
        ),
      ),
    );
  }
}
Optimizing List Performance 🚀

Using ListView.builder for better performance with large lists:
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
          title: Text('Optimized List Example'),
        ),
        body: ListView.builder(
          itemCount: 1000, // Number of items
          itemBuilder: (context, index) {
            return ListTile(
              title: Text('Item $index'),
            );
          },
        ),
      ),
    );
  }
}