# Lesson 4: Practical Examples

**Objective:** Build a savings system using SQLite.

## Savings System

```dart
class SavingsDatabase {
  Future<Database> _initDatabase() async {
    String path = join(await getDatabasesPath(), 'savings.db');
    return openDatabase(
      path,
      onCreate: (db, version) {
        return db.execute('CREATE TABLE savings(id INTEGER PRIMARY KEY, amount REAL, date TEXT)');
      },
      version: 1,
    );
  }

  Future<void> addSaving(double amount, String date) async {
    final db = await _initDatabase();
    await db.insert('savings', {'amount': amount, 'date': date}, conflictAlgorithm: ConflictAlgorithm.replace);
  }

  Future<List<Map<String, dynamic>>> getSavings() async {
    final db = await _initDatabase();
    return db.query('savings');
  }

  Future<void> updateSaving(int id, double amount, String date) async {
    final db = await _initDatabase();
    await db.update('savings', {'amount': amount, 'date': date}, where: 'id = ?', whereArgs: [id]);
  }

  Future<void> deleteSaving(int id) async {
    final db = await _initDatabase();
    await db.delete('savings', where: 'id = ?', whereArgs: [id]);
  }
}
```

### Usage Example

```dart
void main() async {
  final savingsDB = SavingsDatabase();

  // Add a saving entry
  await savingsDB.addSaving(100.50, '2023-07-15');

  // Get all savings
  List<Map<String, dynamic>> savings = await savingsDB.getSavings();
  print(savings);

  // Update a saving entry
  await savingsDB.updateSaving(1, 150.75, '2023-08-01');

  // Delete a saving entry
  await savingsDB.deleteSaving(1);
}
```

### Complete App with UI

Below is a complete example of a Flutter app that uses SQLite to save, delete, and update savings data. It includes a UI that handles these operations.

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
      home: SavingsScreen(),
    );
  }
}

class SavingsScreen extends StatefulWidget {
  @override
  _SavingsScreenState createState() => _SavingsScreenState();
}

class _SavingsScreenState extends State<SavingsScreen> {
  Database? _database;
  List<Map<String, dynamic>> _savings = [];
  TextEditingController _amountController = TextEditingController();
  TextEditingController _dateController = TextEditingController();

  @override
  void initState() {
    super.initState();
    _initDatabase().then((db) {
      _database = db;
      _refreshSavings();
    });
  }

  Future<Database> _initDatabase() async {
    String path = join(await getDatabasesPath(), 'savings.db');
    return openDatabase(
      path,
      onCreate: (db, version) {
        return db.execute('CREATE TABLE savings(id INTEGER PRIMARY KEY, amount REAL, date TEXT)');
      },
      version: 1,
    );
  }

  Future<void> _refreshSavings() async {
    final savings = await getSavings();
    setState(() {
      _savings = savings;
    });
  }

  Future<void> addSaving(double amount, String date) async {
    final db = await _initDatabase();
    await db.insert('savings', {'amount': amount, 'date': date}, conflictAlgorithm: ConflictAlgorithm.replace);
    _refreshSavings();
  }

  Future<List<Map<String, dynamic>>> getSavings() async {
    final db = await _initDatabase();
    return db.query('savings');
  }

  Future<void> updateSaving(int id, double amount, String date) async {
    final db = await _initDatabase();
    await db.update('savings', {'amount': amount, 'date': date}, where: 'id = ?', whereArgs: [id]);
    _refreshSavings();
  }

  Future<void> deleteSaving(int id) async {
    final db = await _initDatabase();
    await db.delete('savings', where: 'id = ?', whereArgs: [id]);
    _refreshSavings();
  }

  void _showSavingDialog({Map<String, dynamic>? saving}) {
    if (saving != null) {
      _amountController.text = saving['amount'].toString();
      _dateController.text = saving['date'];
    } else {
      _amountController.clear();
      _dateController.clear();
    }

    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text(saving == null ? 'Add Saving' : 'Edit Saving'),
        content: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            TextField(
              controller: _amountController,
              decoration: InputDecoration(labelText: 'Amount'),
              keyboardType: TextInputType.number,
            ),
            TextField(
              controller: _dateController,
              decoration: InputDecoration(labelText: 'Date'),
              keyboardType: TextInputType.datetime,
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
              final amount = double.tryParse(_amountController.text) ?? 0.0;
              final date = _dateController.text;

              if (saving == null) {
                addSaving(amount, date);
              } else {
                updateSaving(saving['id'], amount, date);
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
        title: Text('Savings'),
        actions: [
          IconButton(
            icon: Icon(Icons.add),
            onPressed: () => _showSavingDialog(),
          ),
        ],
      ),
      body: ListView.builder(
        itemCount: _savings.length,
        itemBuilder: (context, index) {
          final saving = _savings[index];
          return Dismissible(
            key: ValueKey(saving['id']),
            background: Container(color: Colors.red),
            onDismissed: (direction) {
              deleteSaving(saving['id']);
            },
            child: ListTile(
              title: Text('Amount: \$${saving['amount']}'),
              subtitle: Text('Date: ${saving['date']}'),
              trailing: IconButton(
                icon: Icon(Icons.edit),
                onPressed: () => _showSavingDialog(saving: saving),
              ),
            ),
          );
        },
      ),
    );
  }
}
```

### Example 2: Todo List App

#### Database Initialization

Create a `Todo` table to store todo items.

```dart
Future<Database> initializeTodoDB() async {
  String path = await getDatabasesPath();
  return openDatabase(
    join(path, 'todo_database.db'),
    onCreate: (database, version) async {
      await database.execute(
        "CREATE TABLE todos(id INTEGER PRIMARY KEY AUTOINCREMENT, title TEXT, description TEXT, isComplete INTEGER)",
      );
    },
    version: 1,
  );
}
```

#### CRUD Operations

Implement CRUD operations for the todo items.

```dart
Future<void> insertTodoItem(String title, String description, bool isComplete) async {
  final Database db = await initializeTodoDB();
  await db.insert(
    'todos',
    {'title': title, 'description': description, 'isComplete': isComplete ? 1 : 0},
    conflictAlgorithm: ConflictAlgorithm.replace,
  );
}

Future<List<Map<String, dynamic>>> retrieveTodoItems() async {
  final Database db = await initializeTodoDB();
  return await db.query('todos');
}

Future<void> updateTodoItem(int id, String title, String description, bool isComplete) async {
  final Database db = await initializeTodoDB();
  await db.update(
    'todos',
    {'title': title, 'description': description, 'isComplete': isComplete ? 1 : 0},
    where: 'id = ?',
    whereArgs: [id],
  );
}

Future<void> deleteTodoItem(int id) async {
  final Database db = await initializeTodoDB();
  await db.delete(
    'todos',
    where: 'id = ?',
    whereArgs: [id],
  );
}
```

#### UI Integration

Build a simple UI to display and manage todo items.

```dart
class TodoListPage extends StatefulWidget {
  @override
  _TodoListPageState createState() => _TodoListPageState();
}

class _TodoListPageState extends State<TodoListPage> {
  List<Map<String, dynamic>> _todoItems = [];

  @override
  void initState() {
    super.initState();
    _loadTodoItems();
  }

  void _loadTodoItems() async {
    List<Map<String, dynamic>> items = await retrieveTodoItems();
    setState(() {
      _todoItems = items;
    });
  }

  void _addTodoItem(String title, String description) async {
    await insertTodoItem(title, description, false);
    _loadTodoItems();
  }

  void _updateTodoItem(int id, String title,

 String description, bool isComplete) async {
    await updateTodoItem(id, title, description, isComplete);
    _loadTodoItems();
  }

  void _deleteTodoItem(int id) async {
    await deleteTodoItem(id);
    _loadTodoItems();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Todo List'),
      ),
      body: ListView.builder(
        itemCount: _todoItems.length,
        itemBuilder: (context, index) {
          final todo = _todoItems[index];
          return ListTile(
            title: Text(todo['title']),
            subtitle: Text(todo['description']),
            trailing: Checkbox(
              value: todo['isComplete'] == 1,
              onChanged: (bool? value) {
                _updateTodoItem(
                  todo['id'],
                  todo['title'],
                  todo['description'],
                  value ?? false,
                );
              },
            ),
            onLongPress: () {
              _deleteTodoItem(todo['id']);
            },
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Show dialog to add new todo item
          _showAddTodoDialog();
        },
        child: Icon(Icons.add),
      ),
    );
  }

  void _showAddTodoDialog() {
    TextEditingController titleController = TextEditingController();
    TextEditingController descriptionController = TextEditingController();

    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text('Add Todo Item'),
        content: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            TextField(
              controller: titleController,
              decoration: InputDecoration(labelText: 'Title'),
            ),
            TextField(
              controller: descriptionController,
              decoration: InputDecoration(labelText: 'Description'),
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
              _addTodoItem(titleController.text, descriptionController.text);
              Navigator.of(context).pop();
            },
            child: Text('Save'),
          ),
        ],
      ),
    );
  }
}
```

### Example 3: Contact List App

**Database Initialization**:

Create a `Contact` table to store contact details.

```dart
Future<Database> initializeContactDB() async {
  String path = await getDatabasesPath();
  return openDatabase(
    join(path, 'contact_database.db'),
    onCreate: (database, version) async {
      await database.execute(
        "CREATE TABLE contacts(id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT, phone TEXT)",
      );
    },
    version: 1,
  );
}
```

**CRUD Operations**:

Implement CRUD operations for the contact items.

```dart
Future<void> insertContact(String name, String phone) async {
  final Database db = await initializeContactDB();
  await db.insert(
    'contacts',
    {'name': name, 'phone': phone},
    conflictAlgorithm: ConflictAlgorithm.replace,
  );
}

Future<List<Map<String, dynamic>>> retrieveContacts() async {
  final Database db = await initializeContactDB();
  return await db.query('contacts');
}

Future<void> updateContact(int id, String name, String phone) async {
  final Database db = await initializeContactDB();
  await db.update(
    'contacts',
    {'name': name, 'phone': phone},
    where: 'id = ?',
    whereArgs: [id],
  );
}

Future<void> deleteContact(int id) async {
  final Database db = await initializeContactDB();
  await db.delete(
    'contacts',
    where: 'id = ?',
    whereArgs: [id],
  );
}
```

**UI Integration**:

Build a simple UI to display and manage contact items.

```dart
class ContactListPage extends StatefulWidget {
  @override
  _ContactListPageState createState() => _ContactListPageState();
}

class _ContactListPageState extends State<ContactListPage> {
  List<Map<String, dynamic>> _contacts = [];

  @override
  void initState() {
    super.initState();
    _loadContacts();
  }

  void _loadContacts() async {
    List<Map<String, dynamic>> items = await retrieveContacts();
    setState(() {
      _contacts = items;
    });
  }

  void _addContact(String name, String phone) async {
    await insertContact(name, phone);
    _loadContacts();
  }

  void _updateContact(int id, String name, String phone) async {
    await updateContact(id, name, phone);
    _loadContacts();
  }

  void _deleteContact(int id) async {
    await deleteContact(id);
    _loadContacts();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Contact List'),
      ),
      body: ListView.builder(
        itemCount: _contacts.length,
        itemBuilder: (context, index) {
          final contact = _contacts[index];
          return ListTile(
            title: Text(contact['name']),
            subtitle: Text(contact['phone']),
            trailing: IconButton(
              icon: Icon(Icons.edit),
              onPressed: () {
                _showEditContactDialog(contact);
              },
            ),
            onLongPress: () {
              _deleteContact(contact['id']);
            },
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Show dialog to add new contact
          _showAddContactDialog();
        },
        child: Icon(Icons.add),
      ),
    );
  }

  void _showAddContactDialog() {
    TextEditingController nameController = TextEditingController();
    TextEditingController phoneController = TextEditingController();

    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text('Add Contact'),
        content: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            TextField(
              controller: nameController,
              decoration: InputDecoration(labelText: 'Name'),
            ),
            TextField(
              controller: phoneController,
              decoration: InputDecoration(labelText: 'Phone'),
              keyboardType: TextInputType.phone,
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
              _addContact(nameController.text, phoneController.text);
              Navigator.of(context).pop();
            },
            child: Text('Save'),
          ),
        ],
      ),
    );
  }

  void _showEditContactDialog(Map<String, dynamic> contact) {
    TextEditingController nameController = TextEditingController(text: contact['name']);
    TextEditingController phoneController = TextEditingController(text: contact['phone']);

    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text('Edit Contact'),
        content: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            TextField(
              controller: nameController,
              decoration: InputDecoration(labelText: 'Name'),
            ),
            TextField(
              controller: phoneController,
              decoration: InputDecoration(labelText: 'Phone'),
              keyboardType: TextInputType.phone,
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
              _updateContact(contact['id'], nameController.text, phoneController.text);
              Navigator.of(context).pop();
            },
            child: Text('Save'),
          ),
        ],
      ),
    );
  }
}
```
