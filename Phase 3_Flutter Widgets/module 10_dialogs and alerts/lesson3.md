Lesson 3: BottomSheet
Overview: Creating bottom sheets for additional options, including persistent and modal bottom sheets.

Key Concepts:

Basic Usage of BottomSheet 📜
Creating Persistent and Modal Bottom Sheets 📉
Basic Usage of BottomSheet 📜

Creating a simple BottomSheet:
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
          title: Text('BottomSheet Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              _showBottomSheet(context);
            },
            child: Text('Show BottomSheet'),
          ),
        ),
      ),
    );
  }

  void _showBottomSheet(BuildContext context) {
    showModalBottomSheet(
      context: context,
      builder: (BuildContext context) {
        return Container(
          height: 200,
          color: Colors.white,
          child: Center(
            child: Text('This is a BottomSheet'),
          ),
        );
      },
    );
  }
}
Creating Persistent and Modal Bottom Sheets 📉

Creating a persistent BottomSheet:

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
          title: Text('Persistent BottomSheet Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              _showPersistentBottomSheet(context);
            },
            child: Text('Show Persistent BottomSheet'),
          ),
        ),
      ),
    );
  }

  void _showPersistentBottomSheet(BuildContext context) {
    Scaffold.of(context).showBottomSheet<void>((BuildContext context) {
      return Container(
        height: 200,
        color: Colors.white,
        child: Center(
          child: Text('This is a Persistent BottomSheet'),
        ),
      );
    });
  }
}
Creating a modal BottomSheet:

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
          title: Text('Modal BottomSheet Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              _showModalBottomSheet(context);
            },
            child: Text('Show Modal BottomSheet'),
          ),
        ),
      ),
    );
  }

  void _showModalBottomSheet(BuildContext context) {
    showModalBottomSheet<void>(
      context: context,
      builder: (BuildContext context) {
        return Container(
          height: 200,
          color: Colors.white,
          child: Center(
            child: Text('This is a Modal BottomSheet'),
          ),
        );
      },
    );
  }
}