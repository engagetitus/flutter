Lesson 4: SnackBar and Toast
Overview: Using SnackBar for brief messages and creating toast messages.

Key Concepts:

Basic Usage of SnackBar 🍫
Creating Custom Toast Messages 🍞
Basic Usage of SnackBar 🍫

Showing a simple SnackBar:
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
          title: Text('SnackBar Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              _showSnackBar(context);
            },
            child: Text('Show SnackBar'),
          ),
        ),
      ),
    );
  }

  void _showSnackBar(BuildContext context) {
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(
        content: Text('This is a SnackBar'),
        duration: Duration(seconds: 2),
      ),
    );
  }
}
Creating Custom Toast Messages 🍞

Creating a custom toast message using Overlay:
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
          title: Text('Toast Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              _showToast(context, 'This is a custom toast message');
            },
            child: Text('Show Toast'),
          ),
        ),
      ),
    );
  }

  void _showToast(BuildContext context, String message) {
    OverlayEntry overlayEntry = OverlayEntry(
      builder: (context) => Positioned(
        bottom: 50,
        left: MediaQuery.of(context).size.width / 2 - 100,
        child: Material(
          color: Colors.transparent,
          child: Container(
            padding: EdgeInsets.symmetric(horizontal: 24, vertical: 12),
            decoration: BoxDecoration(
              color: Colors.black,
              borderRadius: BorderRadius.circular(24),
            ),
            child: Text(
              message,
              style: TextStyle(color: Colors.white),
            ),
          ),
        ),
      ),
    );

    Overlay.of(context)?.insert(overlayEntry);

    Future.delayed(Duration(seconds: 2), () {
      overlayEntry.remove();
    });
  }
}