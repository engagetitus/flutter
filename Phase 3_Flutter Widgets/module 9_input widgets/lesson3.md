Lesson 3: Radio Button and Dropdown
Overview: Creating selectable options with Radio and DropdownButton, and managing user selections.

Key Concepts:

Using Radio for Selectable Options 📻
Using DropdownButton for Selectable Options 📂
Using Radio for Selectable Options 📻

Creating a group of radio buttons:
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
          title: Text('Radio Button Example'),
        ),
        body: Center(
          child: StatefulRadio(),
        ),
      ),
    );
  }
}

class StatefulRadio extends StatefulWidget {
  @override
  _StatefulRadioState createState() => _StatefulRadioState();
}

class _StatefulRadioState extends State<StatefulRadio> {
  int _selectedValue = 1;

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        Radio<int>(
          value: 1,
          groupValue: _selectedValue,
          onChanged: (int? value) {
            setState(() {
              _selectedValue = value!;
            });
          },
        ),
        Radio<int>(
          value: 2,
          groupValue: _selectedValue,
          onChanged: (int? value) {
            setState(() {
              _selectedValue = value!;
            });
          },
        ),
      ],
    );
  }
}
Using DropdownButton for Selectable Options 📂

Creating a simple DropdownButton:
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
          title: Text('DropdownButton Example'),
        ),
        body: Center(
          child: StatefulDropdown(),
        ),
      ),
    );
  }
}

class StatefulDropdown extends StatefulWidget {
  @override
  _StatefulDropdownState createState() => _StatefulDropdownState();
}

class _StatefulDropdownState extends State<StatefulDropdown> {
  String _selectedValue = 'One';

  @override
  Widget build(BuildContext context) {
    return DropdownButton<String>(
      value: _selectedValue,
      items: <String>['One', 'Two', 'Three'].map((String value) {
        return DropdownMenuItem<String>(
          value: value,
          child: Text(value),
        );
      }).toList(),
      onChanged: (String? newValue) {
        setState(() {
          _selectedValue = newValue!;
        });
      },
    );
  }
}