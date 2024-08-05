
#### Lesson 2: Managing Focus and Keyboard
- **Overview**: Handling focus and keyboard interactions in Flutter.
- **Key Concepts**:
  - Using `FocusNode` and `FocusScope` 🎯
  - Handling Keyboard Actions ⌨️


# Using `FocusNode` and `FocusScope` 🎯
- **Managing input focus with `FocusNode`**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: FocusNodeScreen(),
      );
    }
  }

  class FocusNodeScreen extends StatelessWidget {
    final FocusNode _focusNode1 = FocusNode();
    final FocusNode _focusNode2 = FocusNode();

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('FocusNode Example'),
        ),
        body: Padding(
          padding: const EdgeInsets.all(16.0),
          child: Column(
            children: [
              TextField(
                focusNode: _focusNode1,
                decoration: InputDecoration(labelText: 'Field 1'),
              ),
              SizedBox(height: 20),
              TextField(
                focusNode: _focusNode2,
                decoration: InputDecoration(labelText: 'Field 2'),
              ),
              SizedBox(height: 20),
              ElevatedButton(
                onPressed: () {
                  FocusScope.of(context).requestFocus(_focusNode2); // Switches focus to Field 2
                },
                child: Text('Focus Field 2'),
              ),
            ],
          ),
        ),
      );
    }
  }
```
Handling Keyboard Actions ⌨️
Customizing keyboard actions and focus changes:
dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: KeyboardActionScreen(),
    );
  }
}

class KeyboardActionScreen extends StatelessWidget {
  final FocusNode _focusNode1 = FocusNode();
  final FocusNode _focusNode2 = FocusNode();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Keyboard Action Example'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              focusNode: _focusNode1,
              decoration: InputDecoration(labelText: 'Field 1'),
              textInputAction: TextInputAction.next, // Moves focus to the next field
              onEditingComplete: () => FocusScope.of(context).requestFocus(_focusNode2),
            ),
            SizedBox(height: 20),
            TextField(
              focusNode: _focusNode2,
              decoration: InputDecoration(labelText: 'Field 2'),
              textInputAction: TextInputAction.done, // Completes the input
              onEditingComplete: () => _focusNode2.unfocus(),
            ),
          ],
        ),
      ),
    );
  }
}
```
