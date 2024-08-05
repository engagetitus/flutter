
#### Lesson 4: Practical Examples with Packages
- **Overview**: Hands-on examples demonstrating the use of various Flutter packages.
- **Key Concepts**:
  - Combining Multiple Packages 📝📝
  - Building a Complete Application with Packages 🗂️


# Combining Multiple Packages 📝📝
- **Using multiple packages in a single project**:
  ```dart
  import 'package:flutter/material.dart';
  import 'package:shared_preferences/shared_preferences.dart';
  import 'package:path_provider/path_provider.dart';
  import 'dart:io';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: CombinedPackagesScreen(),
      );
    }
  }

  class CombinedPackagesScreen extends StatefulWidget {
    @override
    _CombinedPackagesScreenState createState() => _CombinedPackagesScreenState();
  }

  class _CombinedPackagesScreenState extends State<CombinedPackagesScreen> {
    int _counter = 0;
    String _content = '';

    @override
    void initState() {
      super.initState();
      _loadCounter();
      _readContent();
    }

    void _loadCounter() async {
      final prefs = await SharedPreferences.getInstance();
      setState(() {
        _counter = prefs.getInt('counter') ?? 0;
      });
    }

    void _readContent() async {
      final directory = await getApplicationDocumentsDirectory();
      final file = File('${directory.path}/my_file.txt');
      String content = '';
      if (await file.exists()) {
        content = await file.readAsString();
      }
      setState(() {
        _content = content;
      });
    }

    void _incrementCounter() async {
      final prefs = await SharedPreferences.getInstance();
      setState(() {
        _counter++;
        prefs.setInt('counter', _counter);
      });
    }

    void _writeContent() async {
      final directory = await getApplicationDocumentsDirectory();
      final file = File('${directory.path}/my_file.txt');
      await file.writeAsString('Hello, world!');
      _readContent();
    }

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Combined Packages Example'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Text('You have pushed the button this many times:'),
              Text('$_counter', style: Theme.of(context).textTheme.headline4),
              SizedBox(height: 20),
              Text('File content:'),
              Text('$_content', style: Theme.of(context).textTheme.headline4),
            ],
          ),
        ),
        floatingActionButton: Column(
          mainAxisAlignment: MainAxisAlignment.end,
          children: [
            FloatingActionButton(
              onPressed: _incrementCounter,
              tooltip: 'Increment',
              child: Icon(Icons.add),
            ),
            SizedBox(height: 20),
            FloatingActionButton(
              onPressed: _writeContent,
              tooltip: 'Write',
              child: Icon(Icons.save),
            ),
          ],
        ),
      );
    }
  }
```
Building a Complete Application with Packages 🗂️
Creating an application that utilizes multiple packages:

dart

import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';
import 'package:path_provider/path_provider.dart';
import 'dart:io';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CompleteApplicationScreen(),
    );
  }
}

class CompleteApplicationScreen extends StatefulWidget {
  @override
  _CompleteApplicationScreenState createState() => _CompleteApplicationScreenState();
}

class _CompleteApplicationScreenState extends State<CompleteApplicationScreen> {
  int _counter = 0;
  String _content = '';

  @override
  void initState() {
    super.initState();
    _loadCounter();
    _readContent();
  }

  void _loadCounter() async {
    final prefs = await SharedPreferences.getInstance();
    setState(() {
      _counter = prefs.getInt('counter') ?? 0;
    });
  }

  void _readContent() async {
    final directory = await getApplicationDocumentsDirectory();
    final file = File('${directory.path}/my_file.txt');
    String content = '';
    if (await file.exists()) {
      content = await file.readAsString();
    }
    setState(() {
      _content = content;
    });
  }

  void _incrementCounter() async {
    final prefs = await SharedPreferences.getInstance();
    setState(() {
      _counter++;
      prefs.setInt('counter', _counter);
    });
  }

  void _writeContent() async {
    final directory = await getApplicationDocumentsDirectory();
    final file = File('${directory.path}/my_file.txt');
    await file.writeAsString('Hello, world!');
    _readContent();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Complete Application Example'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('You have pushed the button this many times:'),
            Text('$_counter', style: Theme.of(context).textTheme.headline4),
            SizedBox(height: 20),
            Text('File content:'),
            Text('$_content', style: Theme.of(context).textTheme.headline4),
          ],
        ),
      ),
      floatingActionButton: Column(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          FloatingActionButton(
            onPressed: _incrementCounter,
            tooltip: 'Increment',
            child: Icon(Icons.add),
          ),
          SizedBox(height: 20),
          FloatingActionButton(
            onPressed: _writeContent,
            tooltip: 'Write',
            child: Icon(Icons.save),
          ),
        ],
      ),
    );
  }
}
Updating pubspec.yaml:

yaml

dependencies:
  flutter:
    sdk: flutter
  shared_preferences: ^2.0.6
  path_provider: ^2.0.3
  ```

