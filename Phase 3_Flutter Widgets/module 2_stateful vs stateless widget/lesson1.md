
# Lesson 1: Understanding Stateless Widgets

- **Overview**: Introduction to stateless widgets and their usage.
- **Key Concepts**:
  - What is a Stateless Widget? 🧩
  - When to Use Stateless Widgets ⏱️
  - Examples of Stateless Widgets 📝

## What is a Stateless Widget? 🧩

- Stateless widgets are immutable, meaning their properties cannot change once they are set. They are used when the UI depends entirely on the configuration information and not on any dynamic data.

  ```dart
  class MyStatelessWidget extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Text('I am a stateless widget!');
    }
  }

  ```

### When to Use Stateless Widgets ⏱️

Use stateless widgets when the part of the user interface you are describing does not depend on anything other than the configuration information in the object.

### Examples of Stateless Widgets 📝

**Text**: Displays a string of text.

  ```dart

  Text('Hello, world!')
  ```

**Icon**: Displays an icon.

  ``` dart

  Icon(Icons.star)
  ```
