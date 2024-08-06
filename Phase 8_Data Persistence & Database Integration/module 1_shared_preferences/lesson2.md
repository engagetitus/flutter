# Lesson 2: Basic Usage

**Objective:** Learn how to use Shared Preferences to save and retrieve data.

**Topics Covered:**

- Saving data.
- Retrieving data.
- Deleting data.
- Other SharedPreferences methods.

## Saving Data

To store data, use various methods provided by the `SharedPreferences` class.

```dart
Future<void> _saveData(String key, String value) async {
  // Obtain shared preferences
  final prefs = await SharedPreferences.getInstance();
  // Save data with the given key
  prefs.setString(key, value);
}

// Example: Storing different types of data

Future<void> storeData() async {
  // Obtain shared preferences
  SharedPreferences prefs = await SharedPreferences.getInstance();

  // Store a string value
  await prefs.setString('username', 'JohnDoe');

  // Store an integer value
  await prefs.setInt('age', 25);

  // Store a boolean value
  await prefs.setBool('isLoggedIn', true);

  // Store a double value
  await prefs.setDouble('height', 5.9);

  // Store a list of strings
  await prefs.setStringList('favorites', ['Apple', 'Banana', 'Cherry']);
}
```

## Retrieving Data

To retrieve data, use the corresponding getter methods.

```dart
Future<String?> _getData(String key) async {
  // Obtain shared preferences
  final prefs = await SharedPreferences.getInstance();
  // Retrieve data with the given key
  return prefs.getString(key);
}

// Example: Retrieving different types of data

Future<void> retrieveData() async {
  // Obtain shared preferences
  SharedPreferences prefs = await SharedPreferences.getInstance();

  // Retrieve a string value
  String username = prefs.getString('username') ?? 'Guest';

  // Retrieve an integer value
  int age = prefs.getInt('age') ?? 0;

  // Retrieve a boolean value
  bool isLoggedIn = prefs.getBool('isLoggedIn') ?? false;

  // Retrieve a double value
  double height = prefs.getDouble('height') ?? 0.0;

  // Retrieve a list of strings
  List<String> favorites = prefs.getStringList('favorites') ?? [];
}
```

## Deleting Data

To remove data, use the `remove` method.

```dart
Future<void> _deleteData(String key) async {
  // Obtain shared preferences
  final prefs = await SharedPreferences.getInstance();
  // Remove data with the given key
  prefs.remove(key);
}

// Example: Removing data

Future<void> deleteData() async {
  // Obtain shared preferences
  SharedPreferences prefs = await SharedPreferences.getInstance();

  // Remove a specific key-value pair
  await prefs.remove('username');
}
```

## Other SharedPreferences Methods

In addition to saving, retrieving, and deleting data, SharedPreferences provides several other useful methods.

### Checking if a Key Exists

To check if a key exists, use the `containsKey` method.

```dart
Future<bool> _containsKey(String key) async {
  // Obtain shared preferences
  final prefs = await SharedPreferences.getInstance();
  // Check if the key exists
  return prefs.containsKey(key);
}

// Example: Checking for a key

Future<void> checkKey() async {
  // Obtain shared preferences
  SharedPreferences prefs = await SharedPreferences.getInstance();

  // Check if a key exists
  bool hasUsername = prefs.containsKey('username');
  if (hasUsername) {
    print('Username exists');
  } else {
    print('Username does not exist');
  }
}
```

### Getting All Keys

To get all keys, use the `getKeys` method.

```dart
Future<Set<String>> _getAllKeys() async {
  // Obtain shared preferences
  final prefs = await SharedPreferences.getInstance();
  // Get all keys
  return prefs.getKeys();
}

// Example: Retrieving all keys

Future<void> getAllKeys() async {
  // Obtain shared preferences
  SharedPreferences prefs = await SharedPreferences.getInstance();

  // Get all keys
  Set<String> keys = prefs.getKeys();
  keys.forEach((key) {
    print('Key: $key');
  });
}
```

### Clearing All Data

To clear all data, use the `clear` method.

```dart
Future<void> _clearAllData() async {
  // Obtain shared preferences
  final prefs = await SharedPreferences.getInstance();
  // Clear all data
  prefs.clear();
}

// Example: Clearing all data

Future<void> clearData() async {
  // Obtain shared preferences
  SharedPreferences prefs = await SharedPreferences.getInstance();

  // Clear all data
  await prefs.clear();
}
```

### Example App: Simple To-Do List

**Objective:** Create a simple to-do list app that allows users to add, retrieve, and delete tasks using Shared Preferences.

**Features:**

1. Add a task.
2. Retrieve all tasks.
3. Delete a specific task.
4. Delete all tasks.

**Code Example:**

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
      home: TodoList(),
    );
  }
}

class TodoList extends StatefulWidget {
  @override
  _TodoListState createState() => _TodoListState();
}

class _TodoListState extends State<TodoList> {
  TextEditingController _taskController = TextEditingController();
  List<String> _tasks = [];

  @override
  void initState() {
    super.initState();
    _loadTasks();
  }

  Future<void> _loadTasks() async {
    final prefs = await SharedPreferences.getInstance();
    setState(() {
      _tasks = prefs.getStringList('tasks') ?? [];
    });
  }

  Future<void> _addTask(String task) async {
    final prefs = await SharedPreferences.getInstance();
    setState(() {
      _tasks.add(task);
      prefs.setStringList('tasks', _tasks);
    });
  }

  Future<void> _deleteTask(int index) async {
    final prefs = await SharedPreferences.getInstance();
    setState(() {
      _tasks.removeAt(index);
      prefs.setStringList('tasks', _tasks);
    });
  }

  Future<void> _clearAllTasks() async {
    final prefs = await SharedPreferences.getInstance();
    setState(() {
      _tasks.clear();
      prefs.remove('tasks');
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('To-Do List'),
        actions: [
          IconButton(
            icon: Icon(Icons.delete_forever),
            onPressed: _clearAllTasks,
          )
        ],
      ),
      body: Column(
        children: [
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: TextField(
              controller: _taskController,
              decoration: InputDecoration(
                labelText: 'New Task',
                border: OutlineInputBorder(),
              ),
              onSubmitted: (value) {
                if (value.isNotEmpty) {
                  _addTask(value);
                  _taskController.clear();
                }
              },
            ),
          ),
          Expanded(
            child: ListView.builder(
              itemCount: _tasks.length,
              itemBuilder: (context, index) {
                return ListTile(
                  title: Text(_tasks[index]),
                  trailing: IconButton(
                    icon: Icon(Icons.delete),
                    onPressed: () => _deleteTask(index),
                  ),
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

### Task for Reinforcement

**Task:** Extend the To-Do List App

1. **Add Task Timestamp:**
   - Modify the app to store the timestamp of when each task was added.
   - Display the timestamp alongside the task in the list.

2. **Edit Task:**
   - Implement a feature that allows users to edit an existing task.
   - Provide a way for users to update the task text and save changes.

3. **Task Completion Status:**
   - Add a checkbox next to each task to mark it as completed.
   - Save the completion status using Shared Preferences and persist it across app restarts.
   - Style completed tasks with a strikethrough or different color.

### Implementation Hints

1. **Add Task Timestamp:**
   - Use a map to store tasks with their corresponding timestamps.
   - Serialize the map to a JSON string and store it using Shared Preferences.

2. **Edit Task:**
   - Allow users to tap on a task to edit its text.
   - Update the corresponding task in the list and save changes using Shared Preferences.

3. **Task Completion Status:**
   - Use a map or a separate list to store the completion status of each task.
   - Save and retrieve the completion status using Shared Preferences.
   - Update the UI to reflect the completion status of each task.
