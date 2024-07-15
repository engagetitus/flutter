# Session 2: Basic Usage of sqflite 


## Creating Data
To insert data into the database, use the `insert` method.

```dart
Future<void> insertItem(String name, int quantity) async {
  final Database db = await initializeDB();
  await db.insert(
    'items',
    {'name': name, 'quantity': quantity},
    conflictAlgorithm: ConflictAlgorithm.replace,
  );
}
```

## Reading Data
To retrieve data from the database, use the `query` method.

```dart
Future<List<Map<String, dynamic>>> retrieveItems() async {
  final Database db = await initializeDB();
  return await db.query('items');
}
```

## Updating Data
To update existing data, use the `update` method.

```dart
Future<void> updateItem(int id, String name, int quantity) async {
  final Database db = await initializeDB();
  await db.update(
    'items',
    {'name': name, 'quantity': quantity},
    where: 'id = ?',
    whereArgs: [id],
  );
}
```

## Deleting Data
To delete data, use the `delete` method.

```dart
Future<void> deleteItem(int id) async {
  final Database db = await initializeDB();
  await db.delete(
    'items',
    where: 'id = ?',
    whereArgs: [id],
  );
}
```
**Example:**
  ```dart
  SharedPreferences prefs = await SharedPreferences.getInstance();
  await prefs.setString('username', 'JohnDoe');
  String username = prefs.getString('username') ?? 'Guest';
  ```
- **Application:** Save user session data, phone number, and name for feedback.

**2. Storing User Session Data:**
- **Login Example:**
  ```dart
  void _login(String username) async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    await prefs.setString('username', username);
  }

  void _getUserSession() async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    String username = prefs.getString('username') ?? 'Guest';
    print(username);
  }
  ```
