# Lesson 1: Introduction to AnimatedBuilder

Overview: AnimatedBuilder is a powerful widget in Flutter that helps you build complex animations. It separates the animation logic from the widget tree, making your code cleaner and more manageable.

## Key Concepts

- Understanding AnimationController and CurvedAnimation
- Using AnimatedBuilder for Custom Animations
- Understanding AnimationController and CurvedAnimation

In real life, imagine a remote control car. The AnimationController is like the remote control that starts, stops, and changes the speed of the car. The CurvedAnimation is like the terrain on which the car runs, making its movements smoother or more abrupt.

## Setting up AnimationController and CurvedAnimation

```dart

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
          title: Text('AnimatedBuilder Example'),
        ),
        body: Center(
          child: AnimatedBuilderExample(),
        ),
      ),
    );
  }
}

class AnimatedBuilderExample extends StatefulWidget {
  @override
  _AnimatedBuilderExampleState createState() =>_AnimatedBuilderExampleState();
}

class _AnimatedBuilderExampleState extends State<AnimatedBuilderExample> with SingleTickerProviderStateMixin {
  late AnimationController_controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this,
    )..repeat(reverse: true); // Repeats the animation in reverse
    _animation = CurvedAnimation(parent: _controller, curve: Curves.easeInOut); // Applies a smooth curve
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _animation,
      builder: (context, child) {
        return Transform.scale(
          scale:_animation.value, // Scales the child widget based on animation value
          child: FlutterLogo(size: 100),
        );
      },
    );
  }
}
```

## Using AnimatedBuilder for Custom Animations

AnimatedBuilder allows you to create custom animations by rebuilding only the parts of the widget tree that need to be animated.

### Creating a custom animation with AnimatedBuilder

```dart

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
          title: Text('Custom Animation Example'),
        ),
        body: Center(
          child: CustomAnimatedBuilderExample(),
        ),
      ),
    );
  }
}

class CustomAnimatedBuilderExample extends StatefulWidget {
  @override
  _CustomAnimatedBuilderExampleState createState() =>_CustomAnimatedBuilderExampleState();
}

class _CustomAnimatedBuilderExampleState extends State<CustomAnimatedBuilderExample> with SingleTickerProviderStateMixin {
  late AnimationController_controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 3),
      vsync: this,
    )..repeat(reverse: true);
    _animation = CurvedAnimation(parent: _controller, curve: Curves.bounceInOut);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _animation,
      builder: (context, child) {
        return Transform.rotate(
          angle:_animation.value *2.0* 3.141592653589793, // Rotates the child widget
          child: FlutterLogo(size: 100),
        );
      },
    );
  }
}
```
