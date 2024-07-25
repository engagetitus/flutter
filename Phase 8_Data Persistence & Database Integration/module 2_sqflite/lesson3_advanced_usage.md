#### Session 3: Advanced Usage of sqflite 

## Transactions
Use transactions to execute a set of operations atomically.

```dart
Future<void> performTransaction() async {
  final Database db = await initializeDB();
  await db.transaction((txn) async {
    await txn.insert('items', {'name': 'Item 1', 'quantity': 10});
    await txn.insert('items', {'name': 'Item 2', 'quantity': 20});
  });
}
```

## Batch Operations
Use batch operations to execute multiple queries in a single call.

```dart
Future<void> performBatchOperations() async {
  final Database db = await initializeDB();
  var batch = db.batch();
  batch.insert('items', {'name': 'Item 1', 'quantity': 10});
  batch.insert('items', {'name': 'Item 2', 'quantity': 20});
  await batch.commit();
}
```

## Indexing
Create indexes to improve query performance.

```dart
Future<void> createIndex() async {
  final Database db = await initializeDB();
  await db.execute('CREATE INDEX idx_item_name ON items (name)');
}
```

## Error Handling
Handle errors gracefully using try-catch blocks.

```dart
Future<void> insertItemWithErrorHandling(String name, int quantity) async {
  final Database db = await initializeDB();
  try {
    await db.insert(
      'items',
      {'name': name, 'quantity': quantity},
      conflictAlgorithm: ConflictAlgorithm.replace,
    );
  } catch (e) {
    print('Error inserting item: $e');
  }
}
```