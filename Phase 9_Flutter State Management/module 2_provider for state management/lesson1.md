
# Module 2: Provider for State Management

## Lesson 1: Introduction to Provider

### What is Provider?

Provider is a Flutter library used for state management. It allows you to manage and propagate state efficiently and cleanly through your Flutter app.

### Benefits of Using Provider

- Simplifies state management
- Improves code readability and maintainability
- Easily integrates with Flutter’s widget tree

### Setting Up Provider

Add the provider dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  provider: ^6.0.0
```

### Basic Example

``` dart

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

class Counter with ChangeNotifier {
  int _count = 0;
  int get count =>_count;

  void increment() {
    _count++;
    notifyListeners();
  }
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Provider Example')),
        body: Center(
          child: Consumer<Counter>(
            builder: (context, counter, child) {
              return Text('Count: ${counter.count}');
            },
          ),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            Provider.of<Counter>(context, listen: false).increment();
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}
```

## Practical Example: Shopping Cart

```dart

import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

// Product Model
class Product {
  final String name;
  final double price;

  Product(this.name, this.price);
}

// Cart Model
class Cart with ChangeNotifier {
  List<Product> _items = [];

  List<Product> get items => _items;

  void addProduct(Product product) {
    _items.add(product);
    notifyListeners();
  }

  double get total {
    return _items.fold(0, (sum, item) => sum + item.price);
  }
}
```

```dart

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => Cart(),
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Provider Cart Example')),
        body: Column(
          children: [
            Expanded(
              child: ProductList(),
            ),
            CartTotal(),
          ],
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            Provider.of<Cart>(context, listen: false).addProduct(
              Product('Item ${context.read<Cart>().items.length + 1}', 20.0),
            );
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}

class ProductList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<Cart>(
      builder: (context, cart, child) {
        return ListView.builder(
          itemCount: cart.items.length,
          itemBuilder: (context, index) {
            return ListTile(
              title: Text(cart.items[index].name),
              trailing: Text('\$${cart.items[index].price}'),
            );
          },
        );
      },
    );
  }
}

class CartTotal extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(8.0),
      child: Consumer<Cart>(
        builder: (context, cart, child) {
          return Text('Total: \$${cart.total}', style: TextStyle(fontSize: 24));
        },
      ),
    );
  }
}
```
