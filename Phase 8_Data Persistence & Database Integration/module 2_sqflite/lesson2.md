# Session 2: Basic Usage of sqflite

## Lesson 2: Basic Usage

**Objective:** Learn how to use SQLite to create, read, update, and delete data.

**Topics Covered:**

- Creating a database.
- Creating tables.
- Inserting data.
- Querying data.
- Updating data.
- Deleting data.

## Creating a Database

Initialize the SQLite database and create a table for storing user data.

```dart
Future<Database> _initDatabase() async {
  String path = join(await getDatabasesPath(), 'my_database.db');
  return openDatabase(
    path,
    onCreate: (db, version) {
      return db.execute(
        'CREATE TABLE users(id INTEGER PRIMARY KEY, name TEXT, age INTEGER)',
      );
    },
    version: 1,
  );
}
```

## Inserting Data

Insert data into the database using the `insert` method.

```dart
Future<void> insertUser(Map<String, dynamic> user) async {
  final db = await _initDatabase();
  await db.insert('users', user, conflictAlgorithm: ConflictAlgorithm.replace);
}
```

## Querying Data

Retrieve data from the database using the `query` method.

```dart
Future<List<Map<String, dynamic>>> getUsers() async {
  final db = await _initDatabase();
  return db.query('users');
}
```

## Updating Data

Update existing data using the `update` method.

```dart
Future<void> updateUser(int id, Map<String, dynamic> user) async {
  final db = await _initDatabase();
  await db.update('users', user, where: 'id = ?', whereArgs: [id]);
}
```

## Deleting Data

Delete data from the database using the `delete` method.

```dart
Future<void> deleteUser(int id) async {
  final db = await _initDatabase();
  await db.delete('users', where: 'id = ?', whereArgs: [id]);
}
```

## Complete App with UI

Below is a complete example of a Flutter app that uses SQLite to save, delete, and update data. It also includes a UI that handles these operations.

```dart
import 'package:flutter/material.dart';
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: UsersScreen(),
    );
  }
}

class UsersScreen extends StatefulWidget {
  @override
  _UsersScreenState createState() => _UsersScreenState();
}

class _UsersScreenState extends State<UsersScreen> {
  Database? _database;
  List<Map<String, dynamic>> _users = [];
  TextEditingController _nameController = TextEditingController();
  TextEditingController _ageController = TextEditingController();

  @override
  void initState() {
    super.initState();
    _initDatabase().then((db) {
      _database = db;
      _refreshUsers();
    });
  }

  Future<Database> _initDatabase() async {
    String path = join(await getDatabasesPath(), 'my_database.db');
    return openDatabase(
      path,
      onCreate: (db, version) {
        return db.execute(
          'CREATE TABLE users(id INTEGER PRIMARY KEY, name TEXT, age INTEGER)',
        );
      },
      version: 1,
    );
  }

  Future<void> _refreshUsers() async {
    final users = await getUsers();
    setState(() {
      _users = users;
    });
  }

  Future<void> insertUser(Map<String, dynamic> user) async {
    await _database?.insert('users', user, conflictAlgorithm: ConflictAlgorithm.replace);
    _refreshUsers();
  }

  Future<List<Map<String, dynamic>>> getUsers() async {
    return await _database?.query('users') ?? [];
  }

  Future<void> updateUser(int id, Map<String, dynamic> user) async {
    await _database?.update('users', user, where: 'id = ?', whereArgs: [id]);
    _refreshUsers();
  }

  Future<void> deleteUser(int id) async {
    await _database?.delete('users', where: 'id = ?', whereArgs: [id]);
    _refreshUsers();
  }

  void _showUserDialog({Map<String, dynamic>? user}) {
    if (user != null) {
      _nameController.text = user['name'];
      _ageController.text = user['age'].toString();
    } else {
      _nameController.clear();
      _ageController.clear();
    }

    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text(user == null ? 'Add User' : 'Edit User'),
        content: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            TextField(
              controller: _nameController,
              decoration: InputDecoration(labelText: 'Name'),
            ),
            TextField(
              controller: _ageController,
              decoration: InputDecoration(labelText: 'Age'),
              keyboardType: TextInputType.number,
            ),
          ],
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
              final name = _nameController.text;
              final age = int.tryParse(_ageController.text) ?? 0;

              if (user == null) {
                insertUser({'name': name, 'age': age});
              } else {
                updateUser(user['id'], {'name': name, 'age': age});
              }

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
        title: Text('Users'),
        actions: [
          IconButton(
            icon: Icon(Icons.add),
            onPressed: () => _showUserDialog(),
          ),
        ],
      ),
      body: ListView.builder(
        itemCount: _users.length,
        itemBuilder: (context, index) {
          final user = _users[index];
          return Dismissible(
            key: ValueKey(user['id']),
            background: Container(color: Colors.red),
            onDismissed: (direction) {
              deleteUser(user['id']);
            },
            child: ListTile(
              title: Text(user['name']),
              subtitle: Text('Age: ${user['age']}'),
              trailing: IconButton(
                icon: Icon(Icons.edit),
                onPressed: () => _showUserDialog(user: user),
              ),
            ),
          );
        },
      ),
    );
  }
}
```
