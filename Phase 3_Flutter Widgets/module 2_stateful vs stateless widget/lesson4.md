# Lesson 4: Practical Examples

Overview: Hands-on examples to demonstrate the use of stateless and stateful widgets.

## Key Concepts

Creating a Counter App Using Stateful Widget 🧮

Creating a Static Label Using Stateless Widget 🏷️

## Creating a Counter App Using Stateful Widget 🧮

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
        title: 'Stateful Widget Demo',
        home: CounterScreen(),
      );
    }
  }

  class CounterScreen extends StatefulWidget {
    @override
    _CounterScreenState createState() => _CounterScreenState();
  }

  class _CounterScreenState extends State<CounterScreen> {
    int _counter = 0;

    void _incrementCounter() {
      setState(() {
        _counter++;
      });
    }

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Counter App'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Text(
                'You have pushed the button this many times:',
              ),
              Text(
                '$_counter',
                style: Theme.of(context).textTheme.headline4,
              ),
            ],
          ),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: _incrementCounter,
          tooltip: 'Increment',
          child: Icon(Icons.add),
        ),
      );
    }
  }

```

## Creating a Static Label Using Stateless Widget 🏷️

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
      title: 'Stateless Widget Demo',
      home: LabelScreen(),
    );
  }
}

class LabelScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Label Screen'),
      ),
      body: Center(
        child: Text('This is a stateless widget!'),
      ),
    );
  }
}
```
