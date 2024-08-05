Lesson 4: Slider
Overview: Using Slider for selecting a value from a range and customizing its appearance.

Key Concepts:

Basic Usage of Slider 🎚️
Customizing Slider Appearance 🎨
Basic Usage of Slider 🎚️

Creating a simple Slider:
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
          title: Text('Slider Example'),
        ),
        body: Center(
          child: StatefulSlider(),
        ),
      ),
    );
  }
}

class StatefulSlider extends StatefulWidget {
  @override
  _StatefulSliderState createState() => _StatefulSliderState();
}

class _StatefulSliderState extends State<StatefulSlider> {
  double _sliderValue = 0.0;

  @override
  Widget build(BuildContext context) {
    return Slider(
      value: _sliderValue,
      min: 0,
      max: 100,
      onChanged: (double value) {
        setState(() {
          _sliderValue = value;
        });
      },
    );
  }
}
Customizing Slider Appearance 🎨

Styling the Slider with custom properties:
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
          title: Text('Styled Slider Example'),
        ),
        body: Center(
          child: StatefulStyledSlider(),
        ),
      ),
    );
  }
}

class StatefulStyledSlider extends StatefulWidget {
  @override
  _StatefulStyledSliderState createState() => _StatefulStyledSliderState();
}

class _StatefulStyledSliderState extends State<StatefulStyledSlider> {
  double _sliderValue = 0.0;

  @override
  Widget build(BuildContext context) {
    return Slider(
      value: _sliderValue,
      min: 0,
      max: 100,
      divisions: 10,
      label: '$_sliderValue',
      activeColor: Colors.green,
      inactiveColor: Colors.grey,
      onChanged: (double value) {
        setState(() {
          _sliderValue = value;
        });
      },
    );
  }
}