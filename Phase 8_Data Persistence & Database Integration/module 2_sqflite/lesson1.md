# Module 2: SQLite

## Lesson 1: Introduction to SQLite

**Objective:** Understand the basics of SQLite in Flutter.

**Topics Covered:**

- What is SQLite?
- When to use SQLite.
- Installation and setup.

## What is SQLite?

SQLite is a lightweight, relational database engine that is embedded in Flutter. It is ideal for storing structured data in a local database and supports complex queries and data relationships.

### When to Use SQLite

- **Storing Large Amounts of Structured Data:** Suitable for apps requiring local storage of structured data.
- **Complex Queries and Data Relationships:** Ideal for applications needing relational data models.
- **Offline Data Storage:** Useful for apps that need to function without internet connectivity.

## Installation and Setup

### Step 1: Add Dependencies

Add the `sqflite` and `path` packages to your `pubspec.yaml` file:

```yaml
dependencies:
  sqflite: ^2.3.3+1
  path: ^1.9.0
```

Run `flutter pub get` to install the packages.

### Step 2: Import Packages

Import the necessary packages in your Dart file:

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';
```

### Step 3: Initialize the Database

Before using SQLite, initialize the database. This involves specifying the database path and creating tables.

```dart
Future<Database> initializeDB() async {
  // Get the path to the databases directory
  String path = await getDatabasesPath();
  
  // Open the database and create the table if it doesn't exist
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

## Purpose

The `sqflite` plugin allows Flutter apps to interact with SQLite databases. It is used for storing complex data structures persistently, performing CRUD operations, and organizing data into tables.

### Key Concepts

- **SQLite:** A lightweight, embedded relational database engine.
- **Database Operations:** Supports CRUD (Create, Read, Update, Delete) operations.
- **Tables:** Organize data into tables with rows and columns, each table having a unique schema.

### Example: Database Initialization

Here's an example of how to initialize a SQLite database and create a table:

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

Future<Database> initializeDB() async {
  // Get the path to the databases directory
  String path = await getDatabasesPath();
  
  // Open the database and create the table if it doesn't exist
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
