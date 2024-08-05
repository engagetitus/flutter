Lesson 2: Checkbox and Switch
Overview: Using Checkbox and Switch for boolean input and handling state changes.

Key Concepts:

Using Checkbox for Boolean Input ✅
Using Switch for Boolean Input 🔄
Using Checkbox for Boolean Input ✅

Creating a simple Checkbox:
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
          title: Text('Checkbox Example'),
        ),
        body: Center(
          child: StatefulCheckbox(),
        ),
      ),
    );
  }
}

class StatefulCheckbox extends StatefulWidget {
  @override
  _StatefulCheckboxState createState() => _StatefulCheckboxState();
}

class _StatefulCheckboxState extends State<StatefulCheckbox> {
  bool _isChecked = false;

  @override
  Widget build(BuildContext context) {
    return Checkbox(
      value: _isChecked,
      onChanged: (bool? value) {
        setState(() {
          _isChecked = value!;
        });
      },
    );
  }
}
Using Switch for Boolean Input 🔄

Creating a simple Switch:
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
          title: Text('Switch Example'),
        ),
        body: Center(
          child: StatefulSwitch(),
        ),
      ),
    );
  }
}

class StatefulSwitch extends StatefulWidget {
  @override
  _StatefulSwitchState createState() => _StatefulSwitchState();
}

class _StatefulSwitchState extends State<StatefulSwitch> {
  bool _isSwitched = false;

  @override
  Widget build(BuildContext context) {
    return Switch(
      value: _isSwitched,
      onChanged: (bool value) {
        setState(() {
          _isSwitched = value;
        });
      },
    );
  }
}