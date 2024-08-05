# Lesson 3: Practical Examples with AnimatedBuilder

Overview: This lesson provides practical examples of using AnimatedBuilder to create real-world animations.

## Key Concepts

- Building a Loading Spinner
- Creating a Custom Progress Bar
- Building a Loading Spinner

### Example of a loading spinner

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
          title: Text('Loading Spinner Example'),
        ),
        body: Center(
          child: LoadingSpinner(),
        ),
      ),
    );
  }
}

class LoadingSpinner extends StatefulWidget {
  @override
  _LoadingSpinnerState createState() => _LoadingSpinnerState();
}

class _LoadingSpinnerState extends State<LoadingSpinner> with SingleTickerProviderStateMixin {
  late AnimationController _controller;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this,
    )..repeat();
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
        return Transform.rotate(
          angle: _controller.value * 2.0 * 3.141592653589793,
          child: Icon(Icons.sync, size: 50),
        );
      },
    );
  }
}
```

**Explanation** The LoadingSpinner rotates indefinitely, providing a visual indication of a loading process.

## Creating a Custom Progress Bar

Example of a custom progress bar

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
          title: Text('Custom Progress Bar Example'),
        ),
        body: Center(
          child: CustomProgressBar(),
        ),
      ),
    );
  }
}

class CustomProgressBar extends StatefulWidget {
  @override
  _CustomProgressBarState createState() =>_CustomProgressBarState();
}

class _CustomProgressBarState extends State<CustomProgressBar> with SingleTickerProviderStateMixin {
  late AnimationController_controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 5),
      vsync: this,
    )..repeat(reverse: true);

    _animation = Tween(begin: 0.0, end: 1.0).animate(_controller);
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
          width: 200,
          height: 20,
          child: Stack(
            children: <Widget>[
              Container(
                width: 200,
                height: 20,
                color: Colors.grey[300],
              ),
              Container(
                width:_animation.value * 200,
                height: 20,
                color: Colors.blue,
              ),
            ],
          ),
        );
      },
    );
  }
}
```

**Explanation:** The CustomProgressBar animates the width of a blue bar to simulate a progress bar.
