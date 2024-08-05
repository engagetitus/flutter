
# Lesson 1: Understanding Container Widget

- **Overview**: Introduction to the `Container` widget and its properties.
- **Key Concepts**:
  - What is a Container Widget? 📦
  - Properties of Container 📝
  - Using Container for Styling and Layout 🎨

# What is a Container Widget? 📦

- The `Container` widget is a versatile widget that can be used for layout and styling.

  ```dart
  Container(
    width: 100,
    height: 100,
    color: Colors.red,
  )

  ```

## Properties of Container 📝

**width**: Sets the width of the container.
**height**: Sets the height of the container.
**color**: Sets the background color of the container.
**padding**: Adds padding inside the container.
**margin**: Adds margin outside the container.
**decoration**: Adds decorations such as border, shadow, and gradient.

## Using Container for Styling and Layout 🎨

Example of a styled container:

```dart

Container(
  width: 100,
  height: 100,
  decoration: BoxDecoration(
    color: Colors.blue,
    border: Border.all(color: Colors.black, width: 2),
    borderRadius: BorderRadius.circular(10),
    boxShadow: [
      BoxShadow(
        color: Colors.grey,
        offset: Offset(4, 4),
        blurRadius: 10,
      ),
    ],
  ),
  child: Center(
    child: Text('Styled Container'),
  ),
)
```
