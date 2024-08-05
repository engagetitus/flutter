
# Lesson 2: Understanding Stateful Widgets

- **Overview**: Introduction to stateful widgets and their usage.
- **Key Concepts**:
  - What is a Stateful Widget? 🧩
  - When to Use Stateful Widgets ⏱️
  - Examples of Stateful Widgets 📝

# What is a Stateful Widget? 🧩

Stateful widgets are dynamic and can change over time. They have a mutable state that can be updated during the widget's lifecycle.

  ```dart
  class MyStatefulWidget extends StatefulWidget {
    @override
    _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
  }

  class _MyStatefulWidgetState extends State<MyStatefulWidget> {
    int _counter = 0;

    void _incrementCounter() {
      setState(() {
        _counter++;
      });
    }

    @override
    Widget build(BuildContext context) {
      return Column(
        children: <Widget>[
          Text('Counter: $_counter'),
          ElevatedButton(
            onPressed: _incrementCounter,
            child: Text('Increment'),
          ),
        ],
      );
    }
  }

  ```

## When to Use Stateful Widgets ⏱️

Use stateful widgets when the part of the user interface you are describing can change dynamically, such as a form that updates in response to user input.

### Examples of Stateful Widgets 📝

**TextField**: Allows users to enter text.

  ```dart

  TextField(
    onChanged: (text) {
      print('Text field value: $text');
    },
  )
  ```

**Checkbox**: A box that can be checked or unchecked.

```dart

Checkbox(
  value: true,
  onChanged: (bool? newValue) {
    // Handle checkbox change
  },
)
```
