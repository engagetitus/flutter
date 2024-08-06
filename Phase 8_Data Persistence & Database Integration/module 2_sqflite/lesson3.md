# Lesson 3: Advanced Usage

**Objective:** Explore more advanced usage scenarios of SQLite.

**Topics Covered:**

- Transactions.
- Complex queries.
- Indexes and foreign keys.
- Batch operations.
- Error handling.

## Transactions

### What are Transactions?

Transactions in SQLite allow you to execute a set of database operations atomically. This means that either all operations within the transaction are executed successfully, or none are. Transactions are useful for ensuring data integrity, especially when performing multiple related operations.

### Using Transactions

Here's an example of performing a transaction in SQLite using sqflite:

```dart
Future<void> performTransaction() async {
  final db = await _initDatabase();
  await db.transaction((txn) async {
    await txn.insert('users', {'id': 1, 'name': 'Alice', 'age': 24});
    await txn.insert('users', {'id': 2, 'name': 'Bob', 'age': 28});
  });
}
```

## Complex Queries

### What are Complex Queries?

Complex queries involve advanced SQL operations such as filtering, joining tables, and aggregating data. They allow you to retrieve specific subsets of data based on certain conditions.

### Example of a Complex Query

Here's an example of a complex query to retrieve users who are 18 years old or older:

```dart
Future<List<Map<String, dynamic>>> getAdultUsers() async {
  final db = await _initDatabase();
  return db.query('users', where: 'age >= ?', whereArgs: [18]);
}
```

## Indexes and Foreign Keys

### What are Indexes?

Indexes in SQLite are used to improve the performance of database queries. An index is a special data structure that stores a subset of columns from a table, which can be searched more quickly than the entire table.

### Creating an Index

Here's an example of creating an index on the `age` column of the `users` table:

```dart
Future<void> createIndex() async {
  final db = await _initDatabase();
  await db.execute('CREATE INDEX idx_age ON users (age)');
}
```

### What are Foreign Keys?

Foreign keys are used to establish relationships between tables. They ensure that the values in a column (or group of columns) match values in a column of another table, enforcing referential integrity.

### Using Foreign Keys

Here's an example of creating a table with a foreign key that references the `id` column in the `users` table:

```dart
Future<void> createForeignKeyTable() async {
  final db = await _initDatabase();
  await db.execute('CREATE TABLE orders(id INTEGER PRIMARY KEY, userId INTEGER, FOREIGN KEY(userId) REFERENCES users(id))');
}
```

## Batch Operations

### What are Batch Operations?

Batch operations allow you to execute multiple SQL statements in a single call, which can improve performance by reducing the overhead of multiple database round-trips.

### Example of Batch Operations

Here's an example of performing batch operations in SQLite:

```dart
Future<void> performBatchOperations() async {
  final db = await _initDatabase();
  var batch = db.batch();
  batch.insert('users', {'name': 'Item 1', 'quantity': 10});
  batch.insert('users', {'name': 'Item 2', 'quantity': 20});
  await batch.commit();
}
```

## Error Handling

### What is Error Handling?

Error handling involves capturing and managing errors that occur during database operations. Using try-catch blocks can help you handle exceptions gracefully and ensure that your app remains stable.

### Example of Error Handling

Here's an example of handling errors during a database insert operation:

```dart
Future<void> insertItemWithErrorHandling(String name, int quantity) async {
  final db = await _initDatabase();
  try {
    await db.insert(
      'users',
      {'name': name, 'quantity': quantity},
      conflictAlgorithm: ConflictAlgorithm.replace,
    );
  } catch (e) {
    print('Error inserting item: $e');
  }
}
```

## Complete App with Advanced Features

Below is a complete example of a Flutter app that demonstrates advanced usage scenarios, including transactions, complex queries, indexes, and error handling:

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

  Future<void> performTransaction() async {
    final db = await _initDatabase();
    await db.transaction((txn) async {
      await txn.insert('users', {'id': 1, 'name': 'Alice', 'age': 24});
      await txn.insert('users', {'id': 2, 'name': 'Bob', 'age': 28});
    });
  }

  Future<void> createIndex() async {
    final db = await _initDatabase();
    await db.execute('CREATE INDEX idx_age ON users (age)');
  }

  Future<void> createForeignKeyTable() async {
    final db = await _initDatabase();
    await db.execute('CREATE TABLE orders(id INTEGER PRIMARY KEY, userId INTEGER, FOREIGN KEY(userId) REFERENCES users(id))');
  }

  Future<List<Map<String, dynamic>>> getAdultUsers() async {
    final db = await _initDatabase();
    return db.query('users', where: 'age >= ?', whereArgs: [18]);
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
