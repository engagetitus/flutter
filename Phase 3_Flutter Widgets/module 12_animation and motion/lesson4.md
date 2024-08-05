Lesson 4: AnimationController
Overview: Controlling animations with AnimationController and practical examples.

Key Concepts:

Basic Usage of AnimationController 🎛️
Practical Examples with AnimationController 🎥
Basic Usage of AnimationController 🎛️

Creating a simple AnimationController:
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
          title: Text('AnimationController Example'),
        ),
        body: Center(
          child: StatefulAnimationController(),
        ),
      ),
    );
  }
}

class StatefulAnimationController extends StatefulWidget {
  @override
  _StatefulAnimationControllerState createState() => _StatefulAnimationControllerState();
}

class _StatefulAnimationControllerState extends State<StatefulAnimationController> with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this,
    )..repeat(reverse: true);
    _animation = CurvedAnimation(parent: _controller, curve: Curves.easeInOut);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return ScaleTransition(
      scale: _animation,
      child: FlutterLogo(size: 100),
    );
  }
}
Practical Examples with AnimationController 🎥

Combining AnimationController with other widgets:
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
          title: Text('Practical AnimationController Example'),
        ),
        body: Center(
          child: StatefulPracticalAnimationController(),
        ),
      ),
    );
  }
}

class StatefulPracticalAnimationController extends StatefulWidget {
  @override
  _StatefulPracticalAnimationControllerState createState() => _StatefulPracticalAnimationControllerState();
}

class _StatefulPracticalAnimationControllerState extends State<StatefulPracticalAnimationController> with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this,
    )..repeat(reverse: true);
    _animation = CurvedAnimation(parent: _controller, curve: Curves.easeInOut);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return RotationTransition(
      turns: _animation,
      child: FlutterLogo(size: 100),
    );
  }
}