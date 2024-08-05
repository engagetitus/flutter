
# Lesson 4: Practical Flex, Expanded, and Alignment

**Overview**: Hands-on examples to demonstrate the use of flex, expanded, and alignment.
**Key Concepts**:

- Creating a Responsive Layout 📱
- Using Flex and Expanded for Complex Layouts 🛠️
- Aligning Widgets in Different Scenarios 🧭

# Creating a Responsive Layout 📱

**Open `lib/main.dart` and modify the code**:

  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        title: 'Flex, Expanded, and Alignment Demo',
        home: ResponsiveScreen(),
      );
    }
  }

  class ResponsiveScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Responsive Layout'),
        ),
        body: Column(
          children: <Widget>[
            Expanded(
              child: Container(
                color: Colors.red,
                child: Text('Expanded 1'),
              ),
            ),
            Expanded(
              child: Container(
                color: Colors.green,
                child: Text('Expanded 2'),
              ),
            ),
            Expanded(
              child: Container(
                color: Colors.blue,
                child: Text('Expanded 3'),
              ),
            ),
          ],
        ),
      );
    }
  }

```

## Using Flex and Expanded for Complex Layouts 🛠️

Open lib/main.dart and modify the code:

```dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Complex Layout',
      home: ComplexLayoutScreen(),
    );
  }
}

class ComplexLayoutScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Complex Layout'),
      ),
      body: Row(
        children: <Widget>[
          Expanded(
            flex: 2,
            child: Container(
              color: Colors.red,
              child: Text('Expanded 1'),
            ),
          ),
          Expanded(
            flex: 1,
            child: Container(
              color: Colors.green,
              child: Text('Expanded 2'),
            ),
          ),
          Expanded(
            flex: 3,
            child: Container(
              color: Colors.blue,
              child: Text('Expanded 3'),
            ),
          ),
        ],
      ),
    );
  }
}
```

## Aligning Widgets in Different Scenarios 🧭

Open lib/main.dart and modify the code:

```dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Widget Alignment',
      home: AlignmentScreen(),
    );
  }
}

class AlignmentScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Alignment Example'),
      ),
      body: Column(
        children: <Widget>[
          Align(
            alignment: Alignment.topLeft,
            child: Text('Top Left'),
          ),
          Align(
            alignment: Alignment.center,
            child: Text('Center'),
          ),
          Align(
            alignment: Alignment.bottomRight,
            child: Text('Bottom Right'),
          ),
        ],
      ),
    );
  }
}
```
