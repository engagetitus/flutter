Lesson 3: Fade and Scale Transition
Overview: Using FadeTransition and ScaleTransition, and combining animations.

Key Concepts:

Basic Usage of FadeTransition 🌫️
Basic Usage of ScaleTransition 🔍
Combining Animations 🎬
Basic Usage of FadeTransition 🌫️

Creating a simple FadeTransition:
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
          title: Text('FadeTransition Example'),
        ),
        body: Center(
          child: StatefulFadeTransition(),
        ),
      ),
    );
  }
}

class StatefulFadeTransition extends StatefulWidget {
  @override
  _StatefulFadeTransitionState createState() => _StatefulFadeTransitionState();
}

class _StatefulFadeTransitionState extends State<StatefulFadeTransition> with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this,
    );
    _animation = CurvedAnimation(parent: _controller, curve: Curves.easeIn);
    _controller.repeat(reverse: true);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return FadeTransition(
      opacity: _animation,
      child: FlutterLogo(size: 100),
    );
  }
}
Basic Usage of ScaleTransition 🔍

Creating a simple ScaleTransition:
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
          title: Text('ScaleTransition Example'),
        ),
        body: Center(
          child: StatefulScaleTransition(),
        ),
      ),
    );
  }
}

class StatefulScaleTransition extends StatefulWidget {
  @override
  _StatefulScaleTransitionState createState() => _StatefulScaleTransitionState();
}

class _StatefulScaleTransitionState extends State<StatefulScaleTransition> with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this,
    );
    _animation = CurvedAnimation(parent: _controller, curve: Curves.easeIn);
    _controller.repeat(reverse: true);
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
Combining Animations 🎬

Combining FadeTransition and ScaleTransition:
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
          title: Text('Combined Transitions Example'),
        ),
        body: Center(
          child: StatefulCombinedTransition(),
        ),
      ),
    );
  }
}

class StatefulCombinedTransition extends StatefulWidget {
  @override
  _StatefulCombinedTransitionState createState() => _StatefulCombinedTransitionState();
}

class _StatefulCombinedTransitionState extends State<StatefulCombinedTransition> with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _fadeAnimation;
  late Animation<double> _scaleAnimation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this,
    );
    _fadeAnimation = CurvedAnimation(parent: _controller, curve: Curves.easeIn);
    _scaleAnimation = CurvedAnimation(parent: _controller, curve: Curves.easeInOut);
    _controller.repeat(reverse: true);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return FadeTransition(
      opacity: _fadeAnimation,
      child: ScaleTransition(
        scale: _scaleAnimation,
        child: FlutterLogo(size: 100),
      ),
    );
  }
}