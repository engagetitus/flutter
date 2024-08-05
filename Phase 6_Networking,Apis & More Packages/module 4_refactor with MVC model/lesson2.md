# Simple ToDo App

Overview: Building a simple ToDo app to practice the concepts learned.

## Key Concepts

- Managing State with Stateful Widgets 📱
- Using ListView for Dynamic Lists 📋
- Managing State with Stateful Widgets 📱

## Creating a simple ToDo app

```dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: ToDoApp(),
    );
  }
}

class ToDoApp extends StatefulWidget {
  @override
  _ToDoAppState createState() => _ToDoAppState();
}

class _ToDoAppState extends State<ToDoApp> {
  final List<String> _todoList = [];
  final TextEditingController _controller = TextEditingController();

  void _addToDo() {
    setState(() {
      _todoList.add(_controller.text);
      _controller.clear();
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('ToDo App'),
      ),
      body: Column(
        children: <Widget>[
          TextField(
            controller: _controller,
            decoration: InputDecoration(labelText: 'Enter ToDo'),
          ),
          ElevatedButton(
            onPressed: _addToDo,
            child: Text('Add ToDo'),
          ),
          Expanded(
            child: ListView.builder(
              itemCount: _todoList.length,
              itemBuilder: (context, index) {
                return ListTile(
                  title: Text(_todoList[index]),
                );
              },
            ),
          ),
        ],
      ),
    );
  }
}
```

### Explanation

A stateful widget manages the state of the ToDo list.
The list of ToDos is displayed using ListView.builder.
