# Lesson 2: Using GridView.builder

Overview: GridView.builder is used for creating grid-based layouts dynamically.

## Key Concepts

- Creating Dynamic Grids 📐
- Customizing Grid Layouts 🎨
- Creating Dynamic Grids 📐

## Creating a dynamic grid with GridView.builder

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
          title: Text('GridView.builder Example'),
        ),
        body: GridView.builder(
          // Grid layout configuration
          gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
            crossAxisCount: 2,
          ),
          // Number of items in the grid
          itemCount: 10,
          // Function to build each item
          itemBuilder: (context, index) {
            return Card(
              child: Center(
                child: Text('Item $index'),
              ),
            );
          },
        ),
      ),
    );
  }
}
```

### Explanation

GridView.builder creates a grid dynamically.  
gridDelegate defines the grid's structure, such as the number of columns.
