Lesson 1: AnimatedContainer
Overview: Animating container properties with practical examples.

Key Concepts:

Basic Usage of AnimatedContainer 📦
Practical Animation Examples 🎥
Basic Usage of AnimatedContainer 📦

Creating a simple AnimatedContainer:
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
          title: Text('AnimatedContainer Example'),
        ),
        body: Center(
          child: StatefulAnimatedContainer(),
        ),
      ),
    );
  }
}

class StatefulAnimatedContainer extends StatefulWidget {
  @override
  _StatefulAnimatedContainerState createState() => _StatefulAnimatedContainerState();
}

class _StatefulAnimatedContainerState extends State<StatefulAnimatedContainer> {
  bool _selected = false;

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        setState(() {
          _selected = !_selected;
        });
      },
      child: AnimatedContainer(
        width: _selected ? 200 : 100,
        height: _selected ? 200 : 100,
        color: _selected ? Colors.blue : Colors.red,
        alignment: _selected ? Alignment.center : AlignmentDirectional.topCenter,
        duration: Duration(seconds: 1),
        curve: Curves.fastOutSlowIn,
        child: FlutterLogo(size: 75),
      ),
    );
  }
}
Practical Animation Examples 🎥

Combining multiple animations in AnimatedContainer:
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
          title: Text('Combined AnimatedContainer Example'),
        ),
        body: Center(
          child: StatefulCombinedAnimatedContainer(),
        ),
      ),
    );
  }
}

class StatefulCombinedAnimatedContainer extends StatefulWidget {
  @override
  _StatefulCombinedAnimatedContainerState createState() => _StatefulCombinedAnimatedContainerState();
}

class _StatefulCombinedAnimatedContainerState extends State<StatefulCombinedAnimatedContainer> {
  bool _selected = false;

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        setState(() {
          _selected = !_selected;
        });
      },
      child: AnimatedContainer(
        width: _selected ? 300 : 100,
        height: _selected ? 100 : 300,
        color: _selected ? Colors.green : Colors.purple,
        alignment: _selected ? Alignment.bottomRight : Alignment.topLeft,
        duration: Duration(seconds: 1),
        curve: Curves.easeInOut,
        child: FlutterLogo(size: 75),
      ),
    );
  }
}