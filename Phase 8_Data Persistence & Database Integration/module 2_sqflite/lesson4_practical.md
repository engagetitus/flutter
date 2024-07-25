# Session 4: Practical Examples of sqflite 


## Example 1: Todo List App

### Database Initialization
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

### CRUD Operations
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

### UI Integration
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

  void _updateTodoItem(int id, String title, String description, bool isComplete) async {
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
          return ListTile(
            title: Text(_todoItems[index]['title']),
            subtitle: Text(_todoItems[index]['description']),
            trailing: Checkbox(
              value: _todoItems[index]['isComplete'] == 1,
              onChanged: (bool value) {
                _updateTodoItem(
                  _todoItems[index]['id'],
                  _todoItems[index]['title'],
                  _todoItems[index]['description'],
                  value,
                );
              },
            ),
            onLongPress: () {
              _deleteTodoItem(_todoItems[index]['id']);
            },
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Show dialog to add new todo item
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

**Example 2: Improving Ecommerce App with Local Storage:**
- **Saving Cart Items:**
  ```dart
  Future<void> saveCartItem(Product product) async {
    final Database db = await initializeDB();
    await db.insert('cart', product.toMap());
  }
  ```
- **Clearing Database after Checkout:**
  ```dart
  Future<void> clearCart() async {
    final Database db = await initializeDB();
    await db.delete('cart');
  }
  ```