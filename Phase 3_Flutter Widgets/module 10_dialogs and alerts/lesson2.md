Lesson 2: SimpleDialog
Overview: Using SimpleDialog for simple choices and practical examples.

Key Concepts:

Basic Usage of SimpleDialog 🎉
Practical Examples with SimpleDialog 🧩
Basic Usage of SimpleDialog 🎉

Creating a simple SimpleDialog:
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
          title: Text('SimpleDialog Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              showDialog(
                context: context,
                builder: (BuildContext context) {
                  return SimpleDialog(
                    title: Text('Simple Dialog'),
                    children: <Widget>[
                      SimpleDialogOption(
                        onPressed: () {
                          Navigator.of(context).pop();
                        },
                        child: Text('Option 1'),
                      ),
                      SimpleDialogOption(
                        onPressed: () {
                          Navigator.of(context).pop();
                        },
                        child: Text('Option 2'),
                      ),
                    ],
                  );
                },
              );
            },
            child: Text('Show SimpleDialog'),
          ),
        ),
      ),
    );
  }
}
Practical Examples with SimpleDialog 🧩

Using SimpleDialog in a real-world scenario:
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
          title: Text('SimpleDialog Practical Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              _showLanguageDialog(context);
            },
            child: Text('Choose Language'),
          ),
        ),
      ),
    );
  }

  void _showLanguageDialog(BuildContext context) {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return SimpleDialog(
          title: Text('Choose Language'),
          children: <Widget>[
            SimpleDialogOption(
              onPressed: () {
                Navigator.of(context).pop();
                _showChoice(context, 'English');
              },
              child: Text('English'),
            ),
            SimpleDialogOption(
              onPressed: () {
                Navigator.of(context).pop();
                _showChoice(context, 'Spanish');
              },
              child: Text('Spanish'),
            ),
            SimpleDialogOption(
              onPressed: () {
                Navigator.of(context).pop();
                _showChoice(context, 'French');
              },
              child: Text('French'),
            ),
          ],
        );
      },
    );
  }

  void _showChoice(BuildContext context, String choice) {
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(
        content: Text('You selected: $choice'),
      ),
    );
  }
}