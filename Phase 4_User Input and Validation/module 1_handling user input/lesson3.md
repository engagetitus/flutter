
#### Lesson 3: Using Controllers
- **Overview**: Managing user input with `TextEditingController`.
- **Key Concepts**:
  - Using `TextEditingController` for Input Management 📝
  - Listening to Text Changes 👂


# Using `TextEditingController` for Input Management 📝
- **Managing input with `TextEditingController`**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: TextEditingControllerScreen(),
      );
    }
  }

  class TextEditingControllerScreen extends StatelessWidget {
    final TextEditingController _controller = TextEditingController();

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('TextEditingController Example'),
        ),
        body: Padding(
          padding: const EdgeInsets.all(16.0),
          child: Column(
            children: [
              TextField(
                controller: _controller,
                decoration: InputDecoration(labelText: 'Enter your name'),
              ),
              SizedBox(height: 20),
              ElevatedButton(
                onPressed: () {
                  print('Entered text: ${_controller.text}'); // Prints the entered text
                },
                child: Text('Submit'),
              ),
            ],
          ),
        ),
      );
    }
  }
```
Listening to Text Changes 👂
Listening to changes in the text field:
dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: TextChangeListenerScreen(),
    );
  }
}

class TextChangeListenerScreen extends StatelessWidget {
  final TextEditingController _controller = TextEditingController();

  @override
  void initState() {
    _controller.addListener(_printLatestValue); // Adds listener to the controller
  }

  @override
  void dispose() {
    _controller.dispose(); // Disposes the controller
  }

  _printLatestValue() {
    print('Second text field: ${_controller.text}'); // Prints the latest text
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Text Change Listener Example'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: _controller,
              decoration: InputDecoration(labelText: 'Enter text'),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                print('Entered text: ${_controller.text}');
              },
              child: Text('Submit'),
            ),
          ],
        ),
      ),
    );
  }
}
```
