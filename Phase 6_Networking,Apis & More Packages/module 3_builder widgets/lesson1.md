# Lesson 1: Introduction to Builder Widgets

Overview: Builder widgets are powerful tools in Flutter that allow you to create complex UIs by iterating over collections of data.

## Key Concepts

- Using ListView.builder 📋
- Creating Dynamic Lists 📜
- Using ListView.builder 📋

## Creating a dynamic list with ListView.builder

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
          title: Text('ListView.builder Example'),
        ),
        body: ListView.builder(
          // Number of items in the list
          itemCount: 10,
          // Function to build each item
          itemBuilder: (context, index) {
            return ListTile(
              title: Text('Item $index'),
            );
          },
        ),
      ),
    );
  }
}
```

### Explanation

ListView.builder creates a list on demand, building each item only when it's needed.  
itemBuilder is called for each item in the list.
