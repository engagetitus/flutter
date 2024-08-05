
#### Lesson 3: Advanced Custom Widgets
- **Overview**: Creating more complex custom widgets.
- **Key Concepts**:
  - Composing Widgets 🧩
  - Using InheritedWidget for Data Sharing 📡


# Composing Widgets 🧩
- **Composing complex widgets from simpler ones**:
  ```dart
  import 'package:flutter/material.dart';

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: ComposedWidgetScreen(),
      );
    }
  }

  class ComposedWidgetScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Composed Widget Example'),
        ),
        body: Center(
          child: ComposedWidget(),
        ),
      );
    }
  }

  class ComposedWidget extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          CustomStatelessWidget(text: 'Hello,'),
          CustomStatelessWidget(text: 'Flutter!'),
        ],
      );
    }
  }

  class CustomStatelessWidget extends StatelessWidget {
    final String text;

    CustomStatelessWidget({required this.text});

    @override
    Widget build(BuildContext context) {
      return Text(
        text,
        style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
      );
    }
  }
```
Using InheritedWidget for Data Sharing 📡
Sharing data across the widget tree with InheritedWidget:
dart

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: InheritedWidgetScreen(),
    );
  }
}

class InheritedWidgetScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('InheritedWidget Example'),
      ),
      body: DataProvider(
        data: 'Hello, InheritedWidget!',
        child: DataConsumer(),
      ),
    );
  }
}

class DataProvider extends InheritedWidget {
  final String data;

  DataProvider({required Widget child, required this.data}) : super(child: child);

  @override
  bool updateShouldNotify(DataProvider oldWidget) {
    return data != oldWidget.data;
  }

  static DataProvider? of(BuildContext context) {
    return context.dependOnInheritedWidgetOfExactType<DataProvider>();
  }
}

class DataConsumer extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final dataProvider = DataProvider.of(context);

    return Center(
      child: Text(
        dataProvider?.data ?? 'No data found',
        style: TextStyle(fontSize: 24),
      ),
    );
  }
}
```