
# Lesson 4: Practical Usage of MaterialApp and Scaffold

- **Overview**: Hands-on practice with `MaterialApp` and `Scaffold`.
- **Key Concepts**:
  - Creating a New Flutter Project 📁
  - Implementing `MaterialApp` and `Scaffold` 🛠️
  - Adding Basic Navigation 🛤️

# Creating a New Flutter Project 📁

1. **Create a new project**:

  ```bash
  flutter create scaffold_demo
  cd scaffold_demo
  ```

## Implementing MaterialApp and Scaffold 🛠️

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
      title: 'MaterialApp and Scaffold Demo',
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home Screen'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondScreen()),
            );
          },
          child: Text('Go to Second Screen'),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        child: Icon(Icons.add),
        onPressed: () {
          // Handle button press
        },
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Second Screen'),
      ),
      body: Center(
        child: Text('Welcome to the Second Screen!'),
      ),
    );
  }
}
```

## Adding Basic Navigation 🛤️

Use the Navigator widget to navigate between screens.

``` dart

ElevatedButton(
  onPressed: () {
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => SecondScreen()),
    );
  },
  child: Text('Go to Second Screen'),
);
```
