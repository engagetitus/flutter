
#### Lesson 2: Using Popular Packages
- **Overview**: Introduction to some popular Flutter packages.
- **Key Concepts**:
  - `http` for HTTP Requests 🌐
  - `provider` for State Management 📊


# `http` for HTTP Requests 🌐
- **Using the `http` package to make HTTP requests**:
  ```dart
  import 'package:flutter/material.dart';
  import 'package:http/http.dart' as http;

  void main() {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: HttpExampleScreen(),
      );
    }
  }

  class HttpExampleScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('HTTP Example'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'))
                  .then((response) {
                print(response.body); // Prints the fetched data
              });
            },
            child: Text('Fetch Data'),
          ),
        ),
      );
    }
  }

```
provider for State Management 📊
Using the provider package for state management:

dart

import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => Counter(),
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: ProviderExampleScreen(),
    );
  }
}

class ProviderExampleScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Provider Example'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Consumer<Counter>(
              builder: (context, counter, child) {
                return Text(
                  '${counter.value}',
                  style: Theme.of(context).textTheme.headline4,
                );
              },
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          context.read<Counter>().increment();
        },
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
    );
  }
}

class Counter with ChangeNotifier {
  int _value = 0;

  int get value => _value;

  void increment() {
    _value++;
    notifyListeners(); // Notifies listeners to rebuild the UI
  }
}
Updating pubspec.yaml:

yaml

dependencies:
  flutter:
    sdk: flutter
  provider: ^6.0.0 # Adding the provider package