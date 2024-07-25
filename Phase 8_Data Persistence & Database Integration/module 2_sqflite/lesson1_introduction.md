#### Session 1: Introduction to sqflite 

## Purpose
The sqflite plugin allows Flutter apps to interact with SQLite databases. It is used for storing complex data structures persistently.

## Key Concepts
- **SQLite:** A lightweight database engine.
- **Database Operations:** CRUD (Create, Read, Update, Delete) operations.
- **Tables:** Organize data into tables with rows and columns.

## Installation
To use sqflite in a Flutter app, add the `sqflite` and `path` packages to your `pubspec.yaml` file.

```yaml
dependencies:
  sqflite: ^2.3.3+1
  path: ^1.9.0
```

Then, run `flutter pub get` to install the packages.

## Initialization
Before using sqflite, you need to initialize the database.

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

Future<Database> initializeDB() async {
  String path = await getDatabasesPath();
  return openDatabase(
    join(path, 'app_database.db'),
    onCreate: (database, version) async {
      await database.execute(
        "CREATE TABLE items(id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT, quantity INTEGER)",
      );
    },
    version: 1,
  );
}
```
