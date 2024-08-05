
# Lesson 3: Using Scaffold

- **Overview**: How to use `Scaffold` to create the basic structure of your app.
- **Key Concepts**:
  - Basic Structure of `Scaffold` 🏗️
  - Adding an `AppBar` 🛠️
  - Adding a `FloatingActionButton` 🛸

## Basic Structure of `Scaffold` 🏗️

- The `Scaffold` widget provides a framework to implement the basic material design layout.

  ```dart
  Scaffold(
    appBar: AppBar(
      title: Text('Scaffold Demo'),
    ),
    body: Center(
      child: Text('Hello, Scaffold!'),
    ),
  );

  ```

## Adding an AppBar 🛠️

The AppBar widget is used to create a top navigation bar.

  ```dart

  AppBar(
    title: Text('My AppBar'),
    actions: [
      IconButton(
        icon: Icon(Icons.settings),
        onPressed: () {
          // Handle button press
        },
      ),
    ],
  );
  ```

## Adding a FloatingActionButton 🛸

The FloatingActionButton widget is used to create a circular button for primary actions.

```dart

FloatingActionButton(
  child: Icon(Icons.add),
  onPressed: () {
    // Handle button press
  },
);
```
