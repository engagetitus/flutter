
# Lesson 2: Using Padding and Margin

 **Overview**: How to use padding and margin with `Container` widgets.

 **Key Concepts**:

- Adding Padding Inside Container 🛏️
- Adding Margin Outside Container 🌳
- Combining Padding and Margin 🧩

# Adding Padding Inside Container 🛏️

The `padding` property adds space inside the container.

  ```dart
  Container(
    padding: EdgeInsets.all(10),
    color: Colors.red,
    child: Text('Padded Container'),
  )
  ```

## Adding Margin Outside Container 🌳

The margin property adds space outside the container.

```dart

Container(
  margin: EdgeInsets.all(10),
  color: Colors.green,
  child: Text('Container with Margin'),
)
```

## Combining Padding and Margin 🧩

Example of a container with both padding and margin:

```dart

Container(
  padding: EdgeInsets.all(10),
  margin: EdgeInsets.all(10),
  color: Colors.blue,
  child: Text('Container with Padding and Margin'),
)
```
