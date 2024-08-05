
#### Lesson 4: Practical Examples with Custom Widgets
- **Overview**: Hands-on examples demonstrating custom widget creation.
- **Key Concepts**:
  - Building Reusable Widgets 🧱
  - Combining Custom and Built-in Widgets 🛠️


# Building Reusable Widgets 🧱
- **Creating a reusable button widget**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: ReusableWidgetScreen(),
      );
    }
  }

  class ReusableWidgetScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Reusable Widget Example'),
        ),
        body: Center(
          child: CustomButton(
            text: 'Click Me',
            onPressed: () {
              print('Button clicked');
            },
          ),
        ),
      );
    }
  }

  class CustomButton extends StatelessWidget {
    final String text;
    final VoidCallback onPressed;

    CustomButton({required this.text, required this.onPressed});

    @override
    Widget build(BuildContext context) {
      return ElevatedButton(
        onPressed: onPressed,
        child: Text(text),
      );
    }
  }
```
Combining Custom and Built-in Widgets 🛠️
Creating a complex widget using custom and built-in widgets:
dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CustomComplexWidgetScreen(),
    );
  }
}

class CustomComplexWidgetScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Complex Widget Example'),
      ),
      body: Center(
        child: CustomCard(
          title: 'Flutter',
          description: 'A UI toolkit for building natively compiled applications for mobile, web, and desktop from a single codebase.',
        ),
      ),
    );
  }
}

class CustomCard extends StatelessWidget {
  final String title;
  final String description;

  CustomCard({required this.title, required this.description});

  @override
  Widget build(BuildContext context) {
    return Card(
      child: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: <Widget>[
            Text(
              title,
              style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 10),
            Text(
              description,
              style: TextStyle(fontSize: 16),
            ),
            SizedBox(height: 20),
            CustomButton(
              text: 'Learn More',
              onPressed: () {
                print('Learn More button clicked');
              },
            ),
          ],
        ),
      ),
    );
  }
}

class CustomButton extends StatelessWidget {
  final String text;
  final VoidCallback onPressed;

  CustomButton({required this.text, required this.onPressed});

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: onPressed,
      child: Text(text),
    );
  }
}
```
