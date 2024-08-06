# Lesson 5: Best Practices

**Objective:** Learn the best practices for using SQLite.

## Use Transactions

For multiple operations that need to be atomic (all succeed or all fail), use transactions. Transactions ensure data integrity.

```dart
Future<void> performBatchOperations() async {
  final db = await _initDatabase();
  await db.transaction((txn) async {
    await txn.insert('savings', {'amount': 200.00, 'date': '2023-07-20'});
    await txn.update('savings', {'amount': 250.00, 'date': '2023-07-21'}, where: 'id = ?', whereArgs: [1]);
  });
}
```

### Normalize Data

Use proper database normalization techniques to reduce redundancy and improve data integrity. Ensure that your data schema is designed to avoid duplication of data.

### Backup Database

Regularly backup the database to prevent data loss. Implement a mechanism to export and import database content.

### Optimize Queries

Use indexes and proper query optimization techniques to improve the performance of database operations.

#### Creating an Index

```dart
Future<void> createIndex() async {
  final db = await _initDatabase();
  await db.execute('CREATE INDEX idx_amount ON savings (amount)');
}
```

## Data Size

### Small to Medium Data

Use `sqflite` for small to medium datasets. For very large datasets, consider using a more robust database solution.

## Database Schema

### Schema Design

Design the database schema carefully to avoid the need for complex migrations in the future. Plan the structure of your tables and relationships well.

### Normalization

Normalize data to reduce redundancy and improve data integrity. This involves organizing the data in such a way that it adheres to the rules of normalization (1NF, 2NF, 3NF, etc.).

## Performance

### Indexing

Create indexes for frequently queried columns to improve performance.

### Batch Operations

Use batch operations to perform multiple queries efficiently.

```dart
Future<void> performBatchInsert() async {
  final db = await _initDatabase();
  var batch = db.batch();
  batch.insert('savings', {'amount': 100.00, 'date': '2023-07-15'});
  batch.insert('savings', {'amount': 150.00, 'date': '2023-07-16'});
  await batch.commit();
}
```

## Security

### Encryption

Use encryption to secure sensitive data. This is especially important for protecting user data.

### Access Control

Implement access control mechanisms to prevent unauthorized access to the database.

## Error Handling

### Try-Catch

Use try-catch blocks to handle database errors gracefully.

```dart
Future<void> insertWithErrorHandling(double amount, String date) async {
  final db = await _initDatabase();
  try {
    await db.insert(
      'savings',
      {'amount': amount, 'date': date},
      conflictAlgorithm: ConflictAlgorithm.replace,
    );
  } catch (e) {
    print('Error inserting saving: $e');
  }
}
```

### Logging

Log errors for debugging and monitoring purposes. This helps in tracking down issues when they occur.

## Testing

### Unit Tests

Write unit tests for database operations to ensure that they work as expected.

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

void main() {
  test('Test SQLite Database Operations', () async {
    String path = join(await getDatabasesPath(), 'test_database.db');
    Database db = await openDatabase(
      path,
      onCreate: (db, version) async {
        await db.execute('CREATE TABLE test(id INTEGER PRIMARY KEY, value TEXT)');
      },
      version: 1,
    );

    await db.insert('test', {'id': 1, 'value': 'Test Value'});
    List<Map<String, dynamic>> result = await db.query('test');
    expect(result.length, 1);
    expect(result.first['value'], 'Test Value');
  });
}
```

### Mock Databases

Use mock databases for testing purposes to avoid affecting the actual database.

```dart
import 'package:sqflite_common/sqlite_api.dart';
import 'package:sqflite_common_ffi/sqflite_ffi.dart';

void main() {
  sqfliteFfiInit();
  databaseFactory = databaseFactoryFfi;
  // Now run your tests with the FFI database factory
}
```
