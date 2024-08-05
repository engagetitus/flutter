
#### Lesson 3: Exploring Useful Packages
- **Overview**: Introduction to other useful packages for Flutter development.
- **Key Concepts**:
  - `shared_preferences` for Local Storage 🗄️
  - `path_provider` for File System Access 📁


# `shared_preferences` for Local Storage 🗄️
- **Using the `shared_preferences` package for local storage**:
  ```dart
  import 'package:flutter/material.dart';
  import 'package:shared_preferences/shared_preferences.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: SharedPreferencesExampleScreen(),
      );
    }
  }

  class SharedPreferencesExampleScreen extends StatefulWidget {
    @override
    _SharedPreferencesExampleScreenState createState() => _SharedPreferencesExampleScreenState();
  }

  class _SharedPreferencesExampleScreenState extends State<SharedPreferencesExampleScreen> {
    int _counter = 0;

    @override
    void initState() {
      super.initState();
      _loadCounter();
    }

    // Loading counter value on start
    void _loadCounter() async {
      final prefs = await SharedPreferences.getInstance();
      setState(() {
        _counter = prefs.getInt('counter') ?? 0;
      });
    }

    // Incrementing counter value
    void _incrementCounter() async {
      final prefs = await SharedPreferences.getInstance();
      setState(() {
        _counter++;
        prefs.setInt('counter', _counter);
      });
    }

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('SharedPreferences Example'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Text('You have pushed the button this many times:'),
              Text('$_counter', style: Theme.of(context).textTheme.headline4),
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
path_provider for File System Access 📁
Using the path_provider package for file system access:

dart

import 'package:flutter/material.dart';
import 'package:path_provider/path_provider.dart';
import 'dart:io';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: PathProviderExampleScreen(),
    );
  }
}

class PathProviderExampleScreen extends StatefulWidget {
  @override
  _PathProviderExampleScreenState createState() => _PathProviderExampleScreenState();
}

class _PathProviderExampleScreenState extends State<PathProviderExampleScreen> {
  String _content = '';

  @override
  void initState() {
    super.initState();
    _readContent();
  }

  // Reading content from a file
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

  // Writing content to a file
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
        title: Text('PathProvider Example'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('File content:'),
            Text('$_content', style: Theme.of(context).textTheme.headline4),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _writeContent,
        tooltip: 'Write',
        child: Icon(Icons.save),
      ),
    );
  }
}
Updating pubspec.yaml:

yaml

dependencies:
  flutter:
    sdk: flutter
  shared_preferences: ^2.0.6 # Adding the shared_preferences package
  path_provider: ^2.0.3 # Adding the path_provider package