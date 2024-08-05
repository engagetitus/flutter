
#### Lesson 2: Creating Stateful Widgets
- **Overview**: Building custom stateful widgets in Flutter.
- **Key Concepts**:
  - Understanding State Management 🧠
  - Creating a Stateful Widget 🔄


# Understanding State Management 🧠
- **State management in stateful widgets**:
  - Stateful widgets have two classes: the widget class and the state class.
  - The widget class is immutable, while the state class is mutable and can change over time.

# Creating a Stateful Widget 🔄
- **Building a custom stateful widget**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: CustomStatefulWidgetScreen(),
      );
    }
  }

  class CustomStatefulWidgetScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Custom Stateful Widget'),
        ),
        body: Center(
          child: CustomStatefulWidget(),
        ),
      );
    }
  }

  class CustomStatefulWidget extends StatefulWidget {
    @override
    _CustomStatefulWidgetState createState() => _CustomStatefulWidgetState();
  }

  class _CustomStatefulWidgetState extends State<CustomStatefulWidget> {
    int _counter = 0;

    void _incrementCounter() {
      setState(() {
        _counter++;
      });
    }

    @override
    Widget build(BuildContext context) {
      return Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          Text(
            'You have pushed the button this many times:',
          ),
          Text(
            '$_counter',
            style: Theme.of(context).textTheme.headline4,
          ),
          ElevatedButton(
            onPressed: _incrementCounter,
            child: Text('Increment Counter'),
          ),
        ],
      );
    }
  }
```
