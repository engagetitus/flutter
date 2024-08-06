# Lesson 2: Basic Usage

**Objective:** Learn how to use Hive to save and retrieve data.

**Topics Covered:**

- Opening a box.
- Adding data.
- Retrieving data.
- Deleting data.

## Understanding Hive and Boxes

### REVIEW: What is Hive?

Hive is a lightweight and fast key-value database written in pure Dart. It is a great option for Flutter applications to store data locally. Hive is particularly useful for storing simple, structured data such as settings, user preferences, or small datasets.

### What is a Box?

In Hive, a box is a container that stores data. Think of a box as a table in a traditional SQL database. Each box can store a collection of key-value pairs, where the key is a unique identifier, and the value is the data you want to store. You can create multiple boxes in a Hive database, each for different types of data.

## Opening a Box

To store or retrieve data in Hive, you first need to open a box. This is done using the `openBox` method. Once a box is opened, it remains open until the application is closed.

```dart
var box = await Hive.openBox('myBox');
```

## Adding Data

To add or update data in a Hive box, you use the `put` method, which takes a key and a value. If the key already exists, the value is updated.

```dart
await box.put('name', 'John Doe');
```

## Retrieving Data

To retrieve data from a Hive box, use the `get` method with the key you used to store the data.

```dart
String? name = box.get('name');
```

## Deleting Data

To delete data from a Hive box, use the `delete` method with the key of the data you want to remove.

```dart
await box.delete('name');
```

### Complete App with UI

Below is a complete example of a Flutter app that uses Hive to save, delete, and retrieve data. It includes a UI that handles these operations.

#### Dependencies

First, add the Hive dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  hive: ^2.0.0
  hive_flutter: ^1.0.0

dev_dependencies:
  hive_generator: ^1.0.0
  build_runner: ^2.0.0
```

#### Main Application Code

```dart
import 'package:flutter/material.dart';
import 'package:hive/hive.dart';
import 'package:hive_flutter/hive_flutter.dart';

void main() async {
  await Hive.initFlutter();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HiveExample(),
    );
  }
}

class HiveExample extends StatefulWidget {
  @override
  _HiveExampleState createState() => _HiveExampleState();
}

class _HiveExampleState extends State<HiveExample> {
  late Box box;
  TextEditingController _nameController = TextEditingController();

  @override
  void initState() {
    super.initState();
    _openBox();
  }

  Future<void> _openBox() async {
    box = await Hive.openBox('myBox');
    setState(() {});
  }

  Future<void> _addName(String name) async {
    await box.put('name', name);
    setState(() {});
  }

  String? _getName() {
    return box.get('name');
  }

  Future<void> _deleteName() async {
    await box.delete('name');
    setState(() {});
  }

  void _showNameDialog() {
    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text('Enter Name'),
        content: TextField(
          controller: _nameController,
          decoration: InputDecoration(labelText: 'Name'),
        ),
        actions: [
          TextButton(
            onPressed: () {
              Navigator.of(context).pop();
            },
            child: Text('Cancel'),
          ),
          ElevatedButton(
            onPressed: () {
              _addName(_nameController.text);
              _nameController.clear();
              Navigator.of(context).pop();
            },
            child: Text('Save'),
          ),
        ],
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Hive Example'),
        actions: [
          IconButton(
            icon: Icon(Icons.add),
            onPressed: _showNameDialog,
          ),
        ],
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Name: ${_getName() ?? 'No name saved'}'),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _deleteName,
              child: Text('Delete Name'),
            ),
          ],
        ),
      ),
    );
  }
}
```
