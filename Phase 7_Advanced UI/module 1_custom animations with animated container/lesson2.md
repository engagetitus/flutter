# Lesson 2: Advanced Animation Techniques

Overview: This lesson covers more advanced animation techniques using AnimatedBuilder and other widgets to create complex animations.

## Key Concepts

- Combining Multiple Animations
- Using Tween and TweenSequence
- Combining Multiple Animations

Just like a complex dance routine, combining multiple animations can create a more dynamic and engaging experience.

## Combining scale and rotation animations

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
          title: Text('Combined Animations Example'),
        ),
        body: Center(
          child: CombinedAnimationsExample(),
        ),
      ),
    );
  }
}

class CombinedAnimationsExample extends StatefulWidget {
  @override
  _CombinedAnimationsExampleState createState() =>_CombinedAnimationsExampleState();
}

class _CombinedAnimationsExampleState extends State<CombinedAnimationsExample> with SingleTickerProviderStateMixin {
  late AnimationController_controller;
  late Animation<double> _scaleAnimation;
  late Animation<double>_rotationAnimation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 3),
      vsync: this,
    )..repeat(reverse: true);

    _scaleAnimation = CurvedAnimation(parent: _controller, curve: Curves.easeInOut);
    _rotationAnimation = CurvedAnimation(parent: _controller, curve: Curves.linear);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _controller,
      builder: (context, child) {
        return Transform.scale(
          scale:_scaleAnimation.value,
          child: Transform.rotate(
            angle: _rotationAnimation.value *2.0* 3.141592653589793,
            child: FlutterLogo(size: 100),
          ),
        );
      },
    );
  }
}
```

## Using Tween and TweenSequence

Tweens allow you to define a range of values that can be interpolated over time. TweenSequence allows you to combine multiple tweens.

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
          title: Text('TweenSequence Example'),
        ),
        body: Center(
          child: TweenSequenceExample(),
        ),
      ),
    );
  }
}

class TweenSequenceExample extends StatefulWidget {
  @override
  _TweenSequenceExampleState createState() =>_TweenSequenceExampleState();
}

class _TweenSequenceExampleState extends State<TweenSequenceExample> with SingleTickerProviderStateMixin {
  late AnimationController_controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 3),
      vsync: this,
    )..repeat(reverse: true);

    _animation = TweenSequence([
      TweenSequenceItem(tween: Tween(begin: 0.0, end: 50.0), weight: 50),
      TweenSequenceItem(tween: Tween(begin: 50.0, end: 100.0), weight: 50),
    ]).animate(_controller);
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
        return Container(
          width:_animation.value,
          height: _animation.value,
          color: Colors.blue,
        );
      },
    );
  }
}
```
