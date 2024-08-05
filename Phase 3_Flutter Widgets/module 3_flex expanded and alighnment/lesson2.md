# Lesson 2: Using Expanded Widget

- **Overview**: How to use the `Expanded` widget to create flexible layouts.
- **Key Concepts**:
  - What is Expanded? 🛠️
  - Using Expanded in Rows and Columns ➡️⬇️
  - Combining Expanded with Flex Properties 🔄

## What is Expanded? 🛠️

The `Expanded` widget is used to create flexible children that expand to fill the available space.

  ```dart
  Expanded(
    child: Container(
      color: Colors.red,
      child: Text('Expanded Widget'),
    ),
  )

  ```

Using Expanded in Rows and Columns ➡️⬇️
In a Row:

```dart

Row(
  children: <Widget>[
    Expanded(
      child: Container(
        color: Colors.red,
        child: Text('Child 1'),
      ),
    ),
    Expanded(
      child: Container(
        color: Colors.green,
        child: Text('Child 2'),
      ),
    ),
  ],
)
```

## In a Column

```dart

Column(
  children: <Widget>[
    Expanded(
      child: Container(
        color: Colors.red,
        child: Text('Child 1'),
      ),
    ),
    Expanded(
      child: Container(
        color: Colors.green,
        child: Text('Child 2'),
      ),
    ),
  ],
)
```

## Combining Expanded with Flex Properties 🔄

Use mainAxisAlignment and crossAxisAlignment with Expanded to create complex layouts.

```dart

Row(
  mainAxisAlignment: MainAxisAlignment.spaceAround,
  crossAxisAlignment: CrossAxisAlignment.start,
  children: <Widget>[
    Expanded(
      child: Container(
        color: Colors.red,
        child: Text('Child 1'),
      ),
    ),
    Expanded(
      child: Container(
        color: Colors.green,
        child: Text('Child 2'),
      ),
    ),
  ],
)
```
