# Lesson 1: Introduction to MVC Architecture

Overview: The MVC (Model-View-Controller) architecture helps in separating concerns in an application, making it more maintainable.

## Key Concepts

- Understanding MVC Components 🏛️
- Implementing MVC in Flutter 🧩
- Understanding MVC Components 🏛️

**Model**: Represents the data and business logic.
**View**: Displays the data and sends user actions to the controller.
**Controller**: Acts as an intermediary between the model and the view.
Implementing MVC in Flutter 🧩

## Example of MVC structure

```dart

// Model
class CounterModel {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
  }
}

// View
class CounterView extends StatelessWidget {
  final CounterController controller;

  CounterView(this.controller);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('MVC Example'),
      ),
      body: Center(
        child: Text(
          'Count: ${controller.model.count}',
          style: TextStyle(fontSize: 24),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: controller.increment,
        child: Icon(Icons.add),
      ),
    );
  }
}

// Controller
class CounterController {
  final CounterModel model = CounterModel();

  void increment() {
    model.increment();
  }
}

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final controller = CounterController();

    return MaterialApp(
      home: CounterView(controller),
    );
  }
}
```

### Explanation

The model handles the data and business logic.  
The view displays the data and sends user actions to the controller.  
The controller updates the model based on user actions.
